




整理下android的一些基础知识

##  1. Android



#### 1.Activity
- 1.[Activity的启动流程](1.android/1.Activity/Activity.md)
- 2.[onSaveInstanceState(),onRestoreInstanceState的掉用时机](1.android/1.Activity/Activity.md)
- 3.[activity的启动模式和使用场景](1.android/1.Activity/Activity.md)
- 4.[Activity A跳转Activity B，再按返回键，生命周期执行的顺序](1.android/1.Activity/Activity.md)
- 5.[横竖屏切换,按home键,按返回键,锁屏与解锁屏幕,跳转透明Activity界面,启动一个 Theme 为 Dialog 的 Activity，弹出Dialog时Activity的生命周期](1.android/1.Activity/Activity.md)
- 6.[onStart 和 onResume、onPause 和 onStop 的区别](1.android/1.Activity/Activity.md)
- 7.[Activity之间传递数据的方式Intent是否有大小限制，如果传递的数据量偏大，有哪些方案](1.android/1.Activity/Activity.md)
- 8.[Activity的onNewIntent()方法什么时候会执行](1.android/1.Activity/Activity.md)
- 9.[显示启动和隐式启动](1.android/1.Activity/Activity.md)
- 10.[scheme使用场景,协议格式,如何使用](1.android/1.Activity/Activity.md)
- 11.[ANR 的四种场景](1.android/1.Activity/Activity.md)
- 12.[onCreate和onRestoreInstance方法中恢复数据时的区别](1.android/1.Activity/Activity.md)
- 13.[activty间传递数据的方式](1.android/1.Activity/Activity.md)
- 14.[跨App启动Activity的方式,注意事项](1.android/1.Activity/Activity.md)
- 15.[Activity任务栈是什么](1.android/1.Activity/Activity.md)
- 16.[有哪些Activity常用的标记位Flags](1.android/1.Activity/Activity.md)
- 17.[Activity的数据是怎么保存的,进程被Kill后,保存的数据怎么恢复的](1.android/1.Activity/Activity.md)

#### 2.Service
- 1.[service 的生命周期，两种启动方式的区别](1.android/2.Service/Service.md)
- 2.[Service启动流程](1.android/2.Service/Service.md)
- 3.[Service与Activity怎么实现通信](1.android/2.Service/Service.md)
- 4.[IntentService是什么,IntentService原理，应用场景及其与Service的区别](1.android/2.Service/Service.md)
- 5.[Service 的 onStartCommand 方法有几种返回值?各代表什么意思?](1.android/2.Service/Service.md)
- 6.[bindService和startService混合使用的生命周期以及怎么关闭](1.android/2.Service/Service.md)


#### 3.BroadcastReceiver
- 1.[广播的分类和使用场景](1.android/3.BroadcastReceiver/BroadcastReceiver.md)
- 2.[广播的两种注册方式的区别](1.android/3.BroadcastReceiver/BroadcastReceiver.md)
- 3.[广播发送和接收的原理](1.android/3.BroadcastReceiver/BroadcastReceiver.md)
- 4.[本地广播和全局广播的区别](1.android/3.BroadcastReceiver/BroadcastReceiver.md)


#### 4.ContentProvider
- 1.[什么是ContentProvider及其使用](1.android/4.ContentProvider/ContentProvider.md)
- 2.[ContentProvider,ContentResolver,ContentObserver之间的关系](1.android/4.ContentProvider/ContentProvider.md)
- 3.[ContentProvider的实现原理](1.android/4.ContentProvider/ContentProvider.md)
- 4.[ContentProvider的优点](1.android/4.ContentProvider/ContentProvider.md)
- 5.[Uri 是什么](1.android/4.ContentProvider/ContentProvider.md)


#### 5.Handler
- 1.[Handler的实现原理](1.android/5.Handler/Handler.md)
- 2.[子线程中能不能直接new一个Handler,为什么主线程可以](1.android/5.Handler/Handler.md)  
&nbsp;&nbsp;&nbsp;&nbsp;[主线程的Looper第一次调用loop方法,什么时候,哪个类](1.android/5.Handler/Handler.md)
- 3.[Handler导致的内存泄露原因及其解决方案](1.android/5.Handler/Handler.md)
- 4.[一个线程可以有几个Handler,几个Looper,几个MessageQueue对象](1.android/5.Handler/Handler.md)
- 5.[Message对象创建的方式有哪些 & 区别？](1.android/5.Handler/Handler.md)  
&nbsp;&nbsp;&nbsp;&nbsp;[Message.obtain()怎么维护消息池的](1.android/5.Handler/Handler.md)
- 6.[Handler 有哪些发送消息的方法](1.android/5.Handler/Handler.md)
- 7.[Handler的post与sendMessage的区别和应用场景](1.android/5.Handler/Handler.md)
- 8.[handler postDealy后消息队列有什么变化，假设先 postDelay 10s, 再postDelay 1s, 怎么处理这2条消息](1.android/5.Handler/Handler.md)
- 9.[MessageQueue是什么数据结构](1.android/5.Handler/Handler.md)
- 10.[Handler怎么做到的一个线程对应一个Looper，如何保证只有一个MessageQueue](1.android/5.Handler/Handler.md)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ThreadLocal在Handler机制中的作用](1.android/5.Handler/Handler.md)
- 11.[HandlerThread是什么 & 好处 &原理 & 使用场景](1.android/5.Handler/Handler.md)
- 12.[IdleHandler及其使用场景](1.android/5.Handler/Handler.md)
- 13.[消息屏障,同步屏障机制](1.android/5.Handler/Handler.md)
- 14.[子线程能不能更新UI](1.android/5.Handler/Handler.md)
- 15.[为什么Android系统不建议子线程访问UI](1.android/5.Handler/Handler.md)
- 16.[Android中为什么主线程不会因为Looper.loop()里的死循环卡死](1.android/5.Handler/Handler.md)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[MessageQueue#next 在没有消息的时候会阻塞，如何恢复？](1.android/5.Handler/Handler.md)
- 17.[Handler消息机制中，一个looper是如何区分多个Handler的](1.android/5.Handler/Handler.md)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[当Activity有多个Handler的时候，怎么样区分当前消息由哪个Handler处理](1.android/5.Handler/Handler.md)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[处理message的时候怎么知道是去哪个callback处理的](1.android/5.Handler/Handler.md)
- 18.[Looper.quit/quitSafely的区别](1.android/5.Handler/Handler.md)
- 19.[通过Handler如何实现线程的切换](1.android/5.Handler/Handler.md)
- 20.[Handler 如何与 Looper 关联的](1.android/5.Handler/Handler.md)
- 21.[Looper 如何与 Thread 关联的](1.android/5.Handler/Handler.md)
- 22.[Looper.loop()源码](1.android/5.Handler/Handler.md)
- 23.[MessageQueue的enqueueMessage()方法如何进行线程同步的](1.android/5.Handler/Handler.md)
- 24.[MessageQueue的next()方法内部原理](1.android/5.Handler/Handler.md)
- 25.[子线程中是否可以用MainLooper去创建Handler，Looper和Handler是否一定处于一个线程](1.android/5.Handler/Handler.md)
- 26.[ANR和Handler的联系](1.android/5.Handler/Handler.md)

####  6.View绘制
- 1.[View绘制流程](1.android/6.View绘制/View绘制.md)
- 2.[MeasureSpec是什么](1.android/6.View绘制/View绘制.md)
- 3.[子View创建MeasureSpec创建规则是什么](1.android/6.View绘制/View绘制.md)
- 4.[自定义Viewwrap_content不起作用的原因](1.android/6.View绘制/View绘制.md)
- 5.[在Activity中获取某个View的宽高有几种方法](1.android/6.View绘制/View绘制.md)
- 6.[为什么onCreate获取不到View的宽高](1.android/6.View绘制/View绘制.md)
- 7.[View#post与Handler#post的区别](1.android/6.View绘制/View绘制.md)
- 8.[Android绘制和屏幕刷新机制原理](1.android/6.View绘制/View绘制.md)
- 9.[Choreography原理](1.android/6.View绘制/View绘制.md)
- 10.[什么是双缓冲](1.android/6.View绘制/View绘制.md)
- 11.[为什么使用SurfaceView](1.android/6.View绘制/View绘制.md)
- 12.[什么是SurfaceView](1.android/6.View绘制/View绘制.md)
- 13.[View和SurfaceView的区别](1.android/6.View绘制/View绘制.md)
- 14.[SurfaceView为什么可以直接子线程绘制](1.android/6.View绘制/View绘制.md)
- 15.[SurfaceView、TextureView、SurfaceTexture、GLSurfaceView](1.android/6.View绘制/View绘制.md)
- 16.[getWidth()方法和getMeasureWidth()区别](1.android/6.View绘制/View绘制.md)
- 17.[invalidate() 和 postInvalidate() 的区别](1.android/6.View绘制/View绘制.md)
- 18.[Requestlayout，onlayout，onDraw，DrawChild区别与联系](1.android/6.View绘制/View绘制.md)
- 19.[LinearLayout、FrameLayout 和 RelativeLayout 哪个效率高](1.android/6.View绘制/View绘制.md)
- 20.[LinearLayout的绘制流程](1.android/6.View绘制/View绘制.md)
- 21.[自定义 View 的流程和注意事项](1.android/6.View绘制/View绘制.md)
- 22.[自定义View如何考虑机型适配](1.android/6.View绘制/View绘制.md)
- 23.[自定义控件优化方案](1.android/6.View绘制/View绘制.md)
- 24.invalidate怎么局部刷新
- 25.[View加载流程（setContentView）](1.android/6.View绘制/View绘制.md)






####  7.View事件分发
- 1.[View事件分发机制](1.android/7.View事件分发/View事件分发.md)
- 2.[view的onTouchEvent，OnClickListerner和OnTouchListener的onTouch方法 三者优先级](1.android/7.View事件分发/View事件分发.md)
- 3.[onTouch 和onTouchEvent 的区别](1.android/7.View事件分发/View事件分发.md)
- 4.[ACTION_CANCEL什么时候触发](1.android/7.View事件分发/View事件分发.md)
- 5.[事件是先到DecorView还是先到Window](1.android/7.View事件分发/View事件分发.md)
- 6.[点击事件被拦截，但是想传到下面的View，如何操作](1.android/7.View事件分发/View事件分发.md)
- 7.[如何解决View的事件冲突](1.android/7.View事件分发/View事件分发.md)
- 8.[在 ViewGroup 中的 onTouchEvent 中消费 ACTION_DOWN 事件，ACTION_UP事件是怎么传递](1.android/7.View事件分发/View事件分发.md)
- 9.[Activity ViewGroup和View都不消费ACTION_DOWN,那么ACTION_UP事件是怎么传递的](1.android/7.View事件分发/View事件分发.md)
- 10.[同时对父 View 和子 View 设置点击方法，优先响应哪个](1.android/7.View事件分发/View事件分发.md)
- 11.requestDisallowInterceptTouchEvent的调用时机



####  8.RecycleView

- 1.[RecyclerView的多级缓存机制,每一级缓存具体作用是什么,分别在什么场景下会用到哪些缓存](1.android/8.RecycleView/RecycleView.md)
- 2.[RecyclerView的滑动回收复用机制](1.android/8.RecycleView/RecycleView.md)
- 3.[RecyclerView的刷新回收复用机制](1.android/8.RecycleView/RecycleView.md)
- 4.[RecyclerView 为什么要预布局](1.android/8.RecycleView/RecycleView.md)
- 5.[ListView 与 RecyclerView区别](1.android/8.RecycleView/RecycleView.md)
- 6.[RecyclerView性能优化](1.android/8.RecycleView/RecycleView.md)


####  9.Viewpager&Fragment

- 1.[Fragment的生命周期 & 结合Activity的生命周期](1.android/9.Viewpager&Fragment/Viewpager&Fragment.md)
- 2.[Activity和Fragment的通信方式， Fragment之间如何进行通信](1.android/9.Viewpager&Fragment/Viewpager&Fragment.md)
- 3.[为什么使用Fragment.setArguments(Bundle)传递参数](1.android/9.Viewpager&Fragment/Viewpager&Fragment.md)
- 4.[FragmentPageAdapter和FragmentStatePageAdapter区别及使用场景](1.android/9.Viewpager&Fragment/Viewpager&Fragment.md)
- 5.[Fragment懒加载](1.android/9.Viewpager&Fragment/Viewpager&Fragment.md)
- 6.[ViewPager2与ViewPager区别](1.android/9.Viewpager&Fragment/Viewpager&Fragment.md)
- 7.Fragment嵌套问题

####  10.WebView

- 1.[如何提高WebView加载速度](1.android/10.WebView/WebView.md)
- 2.[WebView与 js的交互](1.android/10.WebView/WebView.md)
- 3.[WebView的漏洞](1.android/10.WebView/WebView.md)
- 4.[JsBridge原理](1.android/10.WebView/WebView.md)


####  11.动画

- 1.[动画的类型](1.android/11.动画/动画.md)
- 2.[补间动画和属性动画的区别](1.android/11.动画/动画.md)
- 3.[ObjectAnimator，ValueAnimator及其区别](1.android/11.动画/动画.md)
- 4.[TimeInterpolator插值器，自定义插值器](1.android/11.动画/动画.md)
- 5.[TypeEvaluator估值器](1.android/11.动画/动画.md)


####  12.Bitmap

- 1.[Bitmap 内存占用的计算](1.android/12.Bitmap/Bitmap.md)
- 2.[getByteCount() & getAllocationByteCount()的区别](1.android/12.Bitmap/Bitmap.md)
- 3.[Bitmap的压缩方式](1.android/12.Bitmap/Bitmap.md)
- 4.[LruCache & DiskLruCache原理](1.android/12.Bitmap/Bitmap.md)
- 5.[如何设计一个图片加载库](1.android/12.Bitmap/Bitmap.md)
- 6.[有一张非常大的图片,如何去加载这张大图片](1.android/12.Bitmap/Bitmap.md)
- 7.[如果把drawable-xxhdpi下的图片移动到drawable-xhdpi下，图片内存是如何变的。](1.android/12.Bitmap/Bitmap.md)
- 8.[如果在hdpi、xxhdpi下放置了图片，加载的优先级。如果是400*800，1080*1920，加载的优先级。](1.android/12.Bitmap/Bitmap.md)



####   13.mvc&mvp&mvvm

- 1.[MVC及其优缺点](1.android/13.mvc&mvp&mvvm/mvc&mvp&mvvm.md)
- 2.[MVP及其优缺点](1.android/13.mvc&mvp&mvvm/mvc&mvp&mvvm.md)
- 3.[MVVM及其优缺点](1.android/13.mvc&mvp&mvvm/mvc&mvp&mvvm.md)
- 4.[MVP如何管理Presenter的生命周期，何时取消网络请求](1.android/13.mvc&mvp&mvvm/mvc&mvp&mvvm.md)



####  14.Binder
- 1.[Android中进程和线程的关系,区别](1.android/14.Binder/Binder.md)
- 2.[为何需要进行IPC,多进程通信可能会出现什么问题](1.android/14.Binder/Binder.md)
- 3.[Android中IPC方式有几种、各种方式优缺点](1.android/14.Binder/Binder.md)
- 4.[为何新增Binder来作为主要的IPC方式](1.android/14.Binder/Binder.md)
- 5.[什么是Binder](1.android/14.Binder/Binder.md)
- 6.[Binder的原理<br/>](1.android/14.Binder/Binder.md)
   &nbsp;&nbsp;&nbsp;&nbsp;[Binder Driver 如何在内核空间中做到一次拷贝的？](1.android/14.Binder/Binder.md)
- 7.[使用Binder进行数据传输的具体过程](1.android/14.Binder/Binder.md)
- 8.[Binder框架中ServiceManager的作用](1.android/14.Binder/Binder.md)
- 9.[什么是AIDL](1.android/14.Binder/Binder.md)
- 10.[AIDL使用的步骤](1.android/14.Binder/Binder.md)
- 11.[AIDL支持哪些数据类型](1.android/14.Binder/Binder.md)
- 12.[AIDL的关键类，方法和工作流程](1.android/14.Binder/Binder.md)
- 13.[如何优化多模块都使用AIDL的情况](1.android/14.Binder/Binder.md)
- 14.[使用 Binder 传输数据的最大限制是多少，被占满后会导致什么问题](1.android/14.Binder/Binder.md)
- 15.[Binder 驱动加载过程中有哪些重要的步骤](1.android/14.Binder/Binder.md)
- 16.[系统服务与bindService启动的服务的区别](1.android/14.Binder/Binder.md)
- 17.[Activity的bindService流程](1.android/14.Binder/Binder.md)
- 18.[不通过AIDL，手动编码来实现Binder的通信](1.android/14.Binder/Binder.md)



####  15.内存泄漏&内存溢出

- 1.[什么是OOM & 什么是内存泄漏以及原因](1.android/15.内存泄漏&内存溢出/内存泄漏&内存溢出.md)
- 2.[Thread是如何造成内存泄露的，如何解决？](1.android/15.内存泄漏&内存溢出/内存泄漏&内存溢出.md)
- 3.[Handler导致的内存泄露的原因以及如何解决](1.android/15.内存泄漏&内存溢出/内存泄漏&内存溢出.md)
- 4.[如何加载Bitmap防止内存溢出](1.android/15.内存泄漏&内存溢出/内存泄漏&内存溢出.md)
- 5.[MVP中如何处理Presenter层以防止内存泄漏的](1.android/15.内存泄漏&内存溢出/内存泄漏&内存溢出.md)

####  16.性能优化

- 1.[内存优化](1.android/16.性能优化/性能优化.md)
- 2.[启动优化](1.android/16.性能优化/性能优化.md)
- 3.[布局加载和绘制优化](1.android/16.性能优化/性能优化.md)
- 4.[卡顿优化](1.android/16.性能优化/性能优化.md)
- 5.[网络优化](1.android/16.性能优化/性能优化.md)






####  17.Window&WindowManager

- 1.[什么是Window](1.android/17.Window&WindowManager/Window&WindowManager.md)
- 2.[什么是WindowManager](1.android/17.Window&WindowManager/Window&WindowManager.md)
- 3.[什么是ViewRootImpl](1.android/17.Window&WindowManager/Window&WindowManager.md)
- 4.[什么是DecorView](1.android/17.Window&WindowManager/Window&WindowManager.md)
- 5.[Activity，View，Window三者之间的关系](1.android/17.Window&WindowManager/Window&WindowManager.md)
- 6.[DecorView什么时候被WindowManager添加到Window中](1.android/17.Window&WindowManager/Window&WindowManager.md)

####  18.WMS
- 1.[什么是WMS](1.android/19.AMS/AMS.md)
- 2.[WMS是如何管理Window的](1.android/19.AMS/AMS.md)
- 3.[IWindowSession是什么，WindowSession的创建过程是怎样的](1.android/19.AMS/AMS.md)
- 4.[WindowToken是什么](1.android/19.AMS/AMS.md)
- 5.[WindowState是什么](1.android/19.AMS/AMS.md)
- 6.[Android窗口大概分为几种？分组原理是什么](1.android/19.AMS/AMS.md)
- 7.[Dialog的Context只能是Activity的Context，不能是Application的Context](1.android/19.AMS/AMS.md)
- 8.[App应用程序如何与SurfaceFlinger通信的](1.android/19.AMS/AMS.md)  
    [View 的绘制是如何把数据传递给 SurfaceFlinger 的](1.android/19.AMS/AMS.md)
- 9.[共享内存的具体实现是什么](1.android/19.AMS/AMS.md)
- 10.[relayout是如何向SurfaceFlinger申请Surface](1.android/19.AMS/AMS.md)
- 11.[什么是Surface](1.android/19.AMS/AMS.md)



####  19.AMS
- 1.[ActivityManagerService是什么？什么时候初始化的？有什么作用？](1.android/19.AMS/AMS.md)
- 2.[ActivityThread是什么?ApplicationThread是什么?他们的区别](1.android/19.AMS/AMS.md)
- 3.[Instrumentation是什么？和ActivityThread是什么关系？](1.android/19.AMS/AMS.md)
- 4.[ActivityManagerService和zygote进程通信是如何实现的](1.android/19.AMS/AMS.md)
- 5.[ActivityRecord、TaskRecord、ActivityStack，ActivityStackSupervisor，ProcessRecord](1.android/19.AMS/AMS.md)
- 6.[ActivityManager、ActivityManagerService、ActivityManagerNative、ActivityManagerProxy的关系](1.android/19.AMS/AMS.md)
- 7.[手写实现简化版AMS](1.android/19.AMS/AMS.md)


####  20.系统启动
- 1.[android系统启动流程](1.android/20.系统启动/系统启动.md)
- 2.[SystemServer，ServiceManager，SystemServiceManager的关系](1.android/20.系统启动/系统启动.md)
- 3.[孵化应用进程这种事为什么不交给SystemServer来做，而专门设计一个Zygote](1.android/20.系统启动/系统启动.md)
- 4.[Zygote的IPC通信机制为什么使用socket而不采用binder](1.android/20.系统启动/系统启动.md)



####  21.App启动&打包&安装
- 1.[应用启动流程](1.android/21.App启动&打包&安装/App启动&打包&安装.md)
- 2.[apk组成和Android的打包流程](1.android/21.App启动&打包&安装/App启动&打包&安装.md)
- 3.[Android的签名机制，签名如何实现的,v2相比于v1签名机制的改变](1.android/21.App启动&打包&安装/App启动&打包&安装.md)
- 4.[APK的安装流程](1.android/21.App启动&打包&安装/App启动&打包&安装.md)



####  22.序列化
- 1.[什么是序列化](1.android/22.序列化/序列化.md)
- 2.[为什么需要使用序列化和反序列化](1.android/22.序列化/序列化.md)
- 3.[序列化的有哪些好处](1.android/22.序列化/序列化.md)
- 4.[Serializable 和 Parcelable 的区别](1.android/22.序列化/序列化.md)
- 5.[什么是serialVersionUID](1.android/22.序列化/序列化.md)
- 6.[为什么还要显示指定serialVersionUID的值?](1.android/22.序列化/序列化.md)


####  23.Art & Dalvik 及其区别
- 1.[Art & Dalvik 及其区别](1.android/23.Dalvik&ART/Dalvik&ART.md)


#### 24.模块化&组件化
- 1.[什么是模块化](1.android/24.模块化&组件化/模块化&组件化.md)
- 2.[什么是组件化](1.android/24.模块化&组件化/模块化&组件化.md)
- 3.[组件化优点和方案](1.android/24.模块化&组件化/模块化&组件化.md)
- 4.[组件独立调试](1.android/24.模块化&组件化/模块化&组件化.md)
- 5.[组件间通信](1.android/24.模块化&组件化/模块化&组件化.md)
- 6.[Aplication动态加载](1.android/24.模块化&组件化/模块化&组件化.md)
- 7.[ARouter原理](1.android/24.模块化&组件化/模块化&组件化.md)


#### 25.热修复&插件化
- 1.[插件化的定义](1.android/25.热修复&插件化/插件化.md)
- 2.[插件化的优势](1.android/25.热修复&插件化/插件化.md)
- 3.[插件化框架对比](1.android/25.热修复&插件化/插件化.md)
- 4.[插件化流程](1.android/25.热修复&插件化/插件化.md)
- 5.[插件化类加载原理](1.android/25.热修复&插件化/插件化.md)
- 6.[插件化资源加载原理](1.android/25.热修复&插件化/插件化.md)
- 7.[插件化Activity加载原理](1.android/25.热修复&插件化/插件化.md)
- 8.[热修复和插件化区别](1.android/25.热修复&插件化/热修复.md)
- 9.[热修复原理](1.android/25.热修复&插件化/热修复.md)


#### 26.AOP
- 1.[AOP是什么](1.android/26.AOP/AOP.md)
- 2.[AOP的优点](1.android/26.AOP/AOP.md)
- 3.[AOP的实现方式,APT,AspectJ,ASM,epic,hook](1.android/26.AOP/AOP.md)

#### 27.jectpack
- 1.[Navigation](1.android/27.jectpack/jetpack.md)
- 2.[DataBinding](1.android/27.jectpack/jetpack.md)
- 3.[Viewmodel](1.android/27.jectpack/jetpack.md)
- 4.[livedata](1.android/27.jectpack/jetpack.md)
- 5.[liferecycle](1.android/27.jectpack/jetpack.md)

#### 28.开源框架
- 1.[Okhttp源码流程,线程池](1.android/28.开源框架/框架.md)
- 2.[Okhttp拦截器,addInterceptor 和 addNetworkdInterceptor区别](1.android/28.开源框架/框架.md)
- 3.[Okhttp责任链模式](1.android/28.开源框架/框架.md)
- 4.[Okhttp缓存怎么处理](1.android/28.开源框架/框架.md)
- 5.[Okhttp连接池和socket复用](1.android/28.开源框架/框架.md)
- 6.[Glide怎么绑定生命周期](1.android/28.开源框架/框架.md)
- 7.[Glide缓存机制,内存缓存，磁盘缓存](1.android/28.开源框架/框架.md)
- 8.[Glide与Picasso的区别](1.android/28.开源框架/框架.md)
- 9.[LruCache原理](1.android/28.开源框架/框架.md)
- 10.[Retrofit源码流程,动态代理](1.android/28.开源框架/框架.md)
- 11.[LeakCanary弱引用,源码流程](1.android/28.开源框架/框架.md)
- 12.Eventbus
- 13.Rxjava

##  2.Java



#### 1.HashMap
- 1.[HashMap原理](2.java/HashMap/Hashmap.md)
- 2.[HashMap中put()如何实现的](2.java/HashMap/Hashmap.md)
- 3.[HashMap中get()如何实现的](2.java/HashMap/Hashmap.md)
- 4.[为什么HashMap线程不安全](2.java/HashMap/Hashmap.md)
- 5.[HashMap1.7和1.8有哪些区别](2.java/HashMap/Hashmap.md)
- 6.[解决hash冲突的时候，为什么用红黑树](2.java/HashMap/Hashmap.md)
- 7.[红黑树的效率高，为什么一开始不用红黑树存储](2.java/HashMap/Hashmap.md)
- 8.[不用红黑树，用二叉查找树可以不](2.java/HashMap/Hashmap.md)
- 9.[为什么阀值是8才转为红黑树](2.java/HashMap/Hashmap.md)
- 10.[为什么退化为链表的阈值是6](2.java/HashMap/Hashmap.md)
- 11.[hash冲突有哪些解决办法](2.java/HashMap/Hashmap.md)
- 12.[HashMap在什么条件下扩容](2.java/HashMap/Hashmap.md)
- 13.[HashMap中hash函数怎么实现的，还有哪些hash函数的实现方式](2.java/HashMap/Hashmap.md)
- 14.[为什么不直接将hashcode作为哈希值去做取模,而是要先高16位异或低16位](2.java/HashMap/Hashmap.md)
- 15.[为什么扩容是2的次幂](2.java/HashMap/Hashmap.md)
- 16.[链表的查找的时间复杂度是多少](2.java/HashMap/Hashmap.md)
- 17.红黑树


#### 2.ArrayList

#### 3.Jvm
- 1.[Jvm的内存模型,每个里面都保存的什么](2.java/JVM/JVM.md)
- 2.[类加载机制的几个阶段加载、验证、准备、解析、初始化、使用、卸载](2.java/JVM/JVM.md)
- 3.[对象实例化时的顺序](2.java/JVM/JVM.md)
- 4.[类加载器,双亲委派及其优势](2.java/JVM/JVM.md)
- 5.[垃圾回收机制](2.java/JVM/JVM.md)

#### 4.多线程
- 1.[Java中创建线程的方式,Callable,Runnable,Future,FutureTask](2.java/多线程/多线程.md)
- 2.线程的几种状态
- 3.[谈谈线程死锁，如何有效的避免线程死锁？](2.java/多线程/多线程.md)
- 4.[如何实现多线程中的同步](2.java/多线程/多线程.md)
- 5.[synchronized和Lock的使用、区别,原理；](2.java/多线程/多线程.md)
- 6.[volatile，synchronized和volatile的区别？为何不用volatile替代synchronized？](2.java/多线程/多线程.md)
- 7.[锁的分类，锁的几种状态，CAS原理](2.java/多线程/多线程.md)
- 8.[为什么会有线程安全？如何保证线程安全](2.java/多线程/多线程.md)
- 9.[sleep()与wait()区别,run和start的区别,notify和notifyall区别,锁池,等待池](2.java/多线程/多线程.md)
- 10.[Java多线程通信](2.java/多线程/多线程.md)
- 11.[为什么Java用线程池](2.java/多线程/多线程.md)
- 12.[Java中的线程池参数,共有几种](2.java/多线程/多线程.md)


#### 5.注解
- 1.[注解的分类和底层实现原理](2.java/注解/注解.md)
- 2.自定义注解

#### 6.反射
- 1.[什么是反射](2.java/反射/反射.md)
- 2.[反射机制的相关类](2.java/反射/反射.md)
- 3.[反射中如何获取Class类的实例](2.java/反射/反射.md)
- 4.[如何获取一个类的属性对象 & 构造器对象 & 方法对象](2.java/反射/反射.md)
- 5.[Class.getField和getDeclaredField的区别，getDeclaredMethod和getMethod的区别](2.java/反射/反射.md)
- 6.[反射机制的优缺点](2.java/反射/反射.md)

#### 7.泛型
#### 8.设计模式






































































































































































































































































































































