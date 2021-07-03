https://blog.csdn.net/my_csdnboke/article/details/106685736

##### 1.什么是Window
视图承载器，是一个视图的顶层窗口， 包含了View并对View进行管理,
是一个抽象类，具体的实现类为PhoneWindow,内部持有DecorView。
通过WindowManager创建，并通过WindowManger将DecorView添加进来。




##### 2.什么是WindowManager
WindowManager是一个接口，继承自只有添加、删除、更新三个方法的ViewManager接口。
它的实现类为WindowManagerImpl，WindowManagerImpl通过WindowManagerGlobal代理实现addView，
最后调用到ViewRootImpl的setView   使ViewRoot和Decorview相关联。如果要对Window进行添加和删除就需要使用WindowManager，
具体的工作则由WMS来处理，WindowManager和WMS通过Binder来进行跨进程通信。





##### 3.什么是ViewRootImpl
ViewRoot是View和WindowManager的桥梁，View通过WindowManager来转接调用ViewRootImpl
 View的三大流程(测量（measure），布局（layout），绘制（draw）)均通过ViewRoot来完成。
 Android的所有触屏事件、按键事件、界面刷新等事件都是通过ViewRoot进行分发的。


##### 4.什么是DecorView
DecorView是FrameLayout的子类，它可以被认为是Android视图树的根节点视图,
一般情况下它内部包含一个竖直方向的LinearLayout，在这个LinearLayout里面有上下三个部分，
上面是个ViewStub,延迟加载的视图（应该是设置ActionBar,根据Theme设置），
中间的是标题栏(根据Theme设置，有的布局没有)，下面的是内容栏。
setContentView就是把需要添加的View的结构添加保存在DecorView中。


##### 5.Activity，View，Window三者之间的关系
Activity并不负责视图控制，它只是控制生命周期和处理事件，Activity中持有的是Window
Window是视图的承载器，内部持有一个 DecorView，而这个DecorView才是 view 的根布局  
View就是视图,在setContentView中将R.layout.activity_main添加到DecorView。



##### 6.DecorView什么时候被WindowManager添加到Window中
即使Activity的布局已经成功添加到DecorView中，DecorView此时还没有添加到Window中  
ActivityThread的handleResumeActivity方法中，首先会调用Activity的onResume方法，接着调用Activity的makeVisible()方法  
makeVisible()中完成了DecorView的添加和显示两个过程









