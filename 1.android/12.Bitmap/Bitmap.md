
https://my.oschina.net/zbj1618/blog/2961367

####  1.Bitmap 内存占用的计算


占用的内存大小 = 像素总数量（图片宽x高）x 每个像素的字节大小

每个像素的字节大小与Bitmap的色彩模式有关

public static final Bitmap.Config ALPHA_8 　//代表8位Alpha位图 每个像素占用1byte内存

public static final Bitmap.Config ARGB_4444 　//代表16位ARGB位图 每个像素占用2byte内存

public static final Bitmap.Config ARGB_8888 　//代表32位ARGB位图 每个像素占用4byte内存

public static final Bitmap.Config RGB_565 　//代表8位RGB位图 每个像素占用2byte内存

假设这张图片是ARGB_8888的，那这张图片占的内存就是 width * height * 4个字节或者  width * height * inTargetDensity /inDensity * 4


**加载一张本地Res、Raw资源图片，得到的是图片的原始尺寸 * 缩放系数(inDensity)**

inTargetDensity 为当前屏幕像素密度(宽平方+高平方)/尺寸。

inDensity默认为图片所在文件夹对应的密度()

densityDpi	 160	240	 320	    480	    640

资源目录dpi	mdpi   hdpi	 xhdpi	xxhdpi	xxxhdpi；

像素密度  5.0英寸的手机的屏幕分辨率为1280x720，那么像素密度为192dpi

占用的内存 =  width * height * targetDensity/inDensity * 一个像素所占的内存

**读取SD卡上的图,得到的是图片的原始尺寸**

占用的内存 =  width * height  * 一个像素所占的内存。

#### 2.getByteCount() & getAllocationByteCount()的区别


如果被复用的Bitmap的内存比待分配内存的Bitmap大

getByteCount()获取到的是当前图片应当所占内存大小

getAllocationByteCount()获取到的是被复用Bitmap真实占用内存大小

在复用Bitmap的情况下，getAllocationByteCount()可能会比getByteCount()大。

#### 3.Bitmap的压缩方式


质量压缩，不会对内存产生影响；

采样率压缩，比例压缩，会对内存产生影响；

**质量压缩**

不会减少图片的像素，它是在保持像素的前提下改变图片的位深及透明度等

图片的长，宽，像素都不变，那么bitmap所占内存大小是不会变的

```
ByteArrayOutputStream baos = new ByteArrayOutputStream();
src.compress(Bitmap.CompressFormat.JPEG, quality, baos);
byte[] bytes = baos.toByteArray();
Bitmap  mBitmap = BitmapFactory.decodeByteArray(bytes, 0, bytes.length);  
```

**RGB_565法**

改变一个像素所占的内存
```
BitmapFactory.Options options2 = new BitmapFactory.Options();
            options2.inPreferredConfig = Bitmap.Config.RGB_565;
bm = BitmapFactory.decodeFile(Environment .getExternalStorageDirectory().getAbsolutePath()
 + "/DCIM/Camera/test.jpg", options2);
 ```



**采样率压缩**

设置inSampleSize的值(int类型)后，假如设为n，则宽和高都为原来的1/n，宽高都减少，内存降低
```
BitmapFactory.Options options = new BitmapFactory.Options();
options.inSampleSize = 2;
bm = BitmapFactory.decodeFile(Environment.getExternalStorageDirectory().getAbsolutePath()+ "/DCIM/Camera/test.jpg", options);
```



**比例压缩**

根据图片的缩放比例进行等比大小的缩小尺寸，从而达到压缩的效果

压缩的图片文件尺寸变小，但是解码成bitmap后占得内存变小

Android中使用Matrix对图像进行缩放、旋转、平移、斜切等变换的。
```
Matrix matrix = new Matrix();
matrix.setScale(0.5f, 0.5f);
bm = Bitmap.createBitmap(bit, 0, 0, bit.getWidth(),bit.getHeight(), matrix, true);
```

#### 4.LruCache & DiskLruCache原理

**LRU（Least Recently Used）**

https://blog.csdn.net/u010983881/article/details/79050209


LruCache的核心思想就是维护一个缓存对象列表，从表尾访问数据，在表头删除数据。对象列表的排列方式是按照访问顺序实现，就是 当访问的数据项在链表中存在时，则将该数据项移动到表尾，否则在表尾新建一个数据项。当链表容量超过一定阈值，则移除表头的数据。

利用LinkedHashMap数组+双向链表的数据结构来实现的。其中双向链表的结构可以实现访问顺序和插入顺序，使得LinkedHashMap中的accessOrder设置为true则为访问顺序，为false，则为插入顺序。

写入缓存

1插入元素，并相应增加当前缓存的容量。

2调用trimToSize()开启一个死循环，不断的从表头删除元素，直到当前缓存的容量小于最大容量为止。

读取缓存

调用LinkedHashMap的get()方法，注意如果该元素存在，这个方法会将该元素移动到表尾.

**DiskLruCache**

https://juejin.cn/post/6844903556705681421#heading-6

https://nich.work/2017/DiskLruCache/

https://www.jianshu.com/p/400bda3e37ed

利用 LinkedHashMap实现算法LRU

DiskLruCache 有三个内部类，分别为 Entry、Snapshot 和 Editor。

Entry是 DiskLruCache 内 LinkedHashMap Value 的基本结构。

**Journal 文件**

DiskLruCache 通过在磁盘中创建并维护一个简单的Journal文件来记录各种缓存操作，。记录的类型有4种，分别为READ、REMOVE、CLEAN和DIRTY。


写入缓存的时候会向journal文件写入一条以DIRTY开头的数据表示正在进行写操作，当写入完毕时，分两种情况：1、写入成功，会向journal文件写入一条以CLEAN开头的文件，其中包括该文件的大小。 2、写入失败，会向journal文件写入一条以REMOVE开头的文件,表示删除了该条缓存。也就是说每次写入缓存总是写入两条操作记录。

读取的时候，会向journal文件写入一条以READ开头的文件,表示进行了读操作

删除的时候，会向journal文件写入一条以REMOVE开头的文件,表示删除了该条缓存

通过journal就记录了所有对缓存的操作。并且按照从上到下的读取顺序记录了对所有缓存的操作频繁度和时间顺序。这样当退出程序再次进来调用缓存时，就可以读取这个文件来知道哪些缓存用的比较频繁了。然后把这些操作记录读取到集合中，操作的时候就可以直接从集合中去对应的数据了。

在缓存记录之外，Journal 文件在初始化创建的时候还有一些固定的头部信息，包括了文件名、版本号和valueCount(决定每一个 key 能匹配的 Entry 数量)。


**读取**

  Snapshot是Entry的快照(snapshot)。当调用 diskLruCache.get(key)时，便能获得一个Snapshot对象，该对象可用于获取或更新存于磁盘的缓存
 ```
  String key = Util.hashKeyForDisk(Util.IMG_URL);
  DiskLruCache.Snapshot snapshot = diskLruCache.get(key);
  if (snapshot != null) {
    InputStream in = snapshot.getInputStream(0);
    return BitmapFactory.decodeStream(in);
  }
```

1获取到缓存文件的输入流，等待被读取。

2向journal写入一行READ开头的记录，表示执行了一次读取操作。

3如果缓存总大小已经超过了设定的最大缓存大小或者操作次数超过了2000次，就开一个线程将集合中的数据删除到小于最大缓存大小为止并重新写journal文件。


4返回缓存文件快照，包含缓存文件大小，输入流等信息。


**写入**


 ```
DiskLruCache.Editor editor = diskLruCache.edit(key);
    if (editor != null) {
        OutputStream outputStream = editor.newOutputStream(0);
        if (downloadUrlToStream(Util.IMG_URL, outputStream)) {
            publishProgress("");
            //写入缓存
            editor.commit();
        } else {
             //写入失败
            editor.abort();
        }
    }
diskLruCache.flush();
 ```


1从集合中找到对应的实例（如果没有创建一个放到集合中），然后创建一个editor，将editor和entry关联起来。


2向journal中写入一行操作数据（DITTY 空格 和key拼接的文字），表示这个key当前正处于编辑状态。


newOutputStream


1向journal文件写入一行CLEAN开头的字符（包括key和文件的大小，文件大小可能存在多个 使用空格分开的）


2重新比较当前缓存和最大缓存的大小，如果超过最大缓存或者journal文件的操作大于2000条，就把集合中的缓存删除一部分，直到小于最大缓存，重新建立新的journal文件


#### 5.如何设计一个图片加载库

https://juejin.cn/post/6844904099297624077#heading-0


1.对图片进行内存压缩；

2.高分辨率的图片放入对应文件夹；

3.缓存

4.及时回收


#### 6.有一张非常大的图片,如何去加载这张大图片




#### 7、如果把drawable-xxhdpi下的图片移动到drawable-xhdpi下，图片内存是如何变的。


验证
    原图：1000宽X447高，位于drawable-xxhdpi（480dpi）文件包，设备Pixel-XL（560dpi）。使用默认Bitmap.Config=ARGB_8888,设置inSampleSize=2

        缩放比=主动设置×被动设置=1/2×(560/480)=0.5×1.166=0.5833
        一个像素所占的内存=ARGB_8888=32bit=4byte
        原始大小=1000×447
    
    width * height *  * 
        内存占用=(原始宽×缩放比)×(原始高×缩放比)×targetDensity/inDensity×一个像素所占的内存  =1000×0.5833×447×0.5833×4  =583×260×4  =606320byte  ≈0.578MB

#### 8、如果在hdpi、xxhdpi下放置了图片，加载的优先级。如果是400*800，1080*1920，加载的优先级。

https://cloud.tencent.com/developer/article/1015960


优先会去更高密度的文件夹下找这张图片，我们当前的场景就是drawable-xxxhdpi文件夹，然后发现这里也没有android_logo这张图，接下来会尝试再找更高密度的文件夹，发现没有更高密度的了，这个时候会去drawable-nodpi文件夹找这张图，发现也没有，那么就会去更低密度的文件夹下面找，依次是drawable-xhdpi -> drawable-hdpi -> drawable-mdpi -> drawable-ldp


0dpi ~ 120dpi   ldpi


120dpi ~ 160dpi  mdpi


160dpi ~ 240dpi hdpi


240dpi ~ 320dpi xhdpi


320dpi ~ 480dpi xxhdpi


480dpi ~ 640dpi  xxxhdpi



