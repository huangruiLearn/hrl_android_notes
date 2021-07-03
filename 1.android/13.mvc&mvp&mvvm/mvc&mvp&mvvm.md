####  1.MVC及其优缺点

原理

视图层(View)

一般采用XML文件进行界面的描述，这些XML可以理解为AndroidApp的View。


控制层(Controller)

Android的控制层的重任通常落在了众多的Activity的肩上。


模型层(Model)

我们针对业务模型，建立的数据结构和相关的类，就可以理解为AndroidApp的Model，Model是与View无关，而与业务相关的。对数据库的操作、对网络等的操作都应该在Model里面处理，当然对业务计算等操作也是必须放在的该层的。

缺点

随着界面及其逻辑的复杂度不断提升，Activity类的职责不断增加，以致变得庞大臃肿。




####  2.MVP及其优缺点

原理

MVP框架由3部分组成：View负责显示，Presenter负责逻辑处理，Model提供数据。

View: 显示数据, 并向Presenter报告用户行为。与用户进行交互(在Android中体现为Activity)。

Presenter: 逻辑处理，从Model拿数据，回显到UI层，响应用户的行为。

Model:负责存储、检索、操纵数据(有时也实现一个Model interface用来降低耦合)。

google todo-mvp加入契约类来统一管理view与presenter的所有的接口，这种方式使得view与presenter中有哪些功能，一目了然

优点

1.分离视图逻辑和业务逻辑，降低了耦合，修改视图而不影响模型，不需要改变Presenter的逻辑
  模型与视图完全分离，我们可以修改视图而不影响模型；


2.视图逻辑和业务逻辑分别抽象到了View和Presenter的接口中，Activity只负责显示，代码变得更加简洁，提高代码的阅读性。

3.Presenter被抽象成接口，可以有多种具体的实现，所以方便进行单元测试。

Presenter是通过interface与View(Activity)进行交互的，这说明我们可以通过自定义类实现这个interface来模拟Activity的行为对Presenter进行单元测试，省去了大量的部署及测试的时间（不需要将应用部署到Android模拟器或真机上，然后通过模拟用 户操作进行测试）

缺点

1.那就是对 UI 的操作必须在 Activity 与 Fragment 的生命周期之内，更细致一点，最好在 onStart() 之后 onPause()之前，否则极其容易出现各种异常，内存泄漏。

2.Presenter与View之间的耦合度高，app中很多界面都使用了同一个Presenter 。一旦需要变更，那么视图需要变更了。

**MVP如何设计避免内存泄漏？**

Mvp模式在封装的时候会造成内存泄漏，因为presenter层，需要做网络请求，所以就需要考虑到网络请求的取消操作，如果不处理，activity销毁了，presenter层还在请求网络，就会造成内存泄漏。
**如何解决Mvp模式造成的内存泄漏？**
只要presenter层能感知activity生命周期的变化，在activity销毁的时候，取消网络请求，就能解决这个问题。
下面开始封装activity和presenter。

**定义IPresenter** 声明activity（Fragment）生命周期中的各个回调方法
```
 <U extends IUI> void init(BaseActivity activity, U ui);

    /**
     * onUICreate:UI被创建的时候应该invoke这个method. <br/>
     * <p/>
     * 比如Activity的onCreate()、Fragment的onCreateView()的方法应该调用Presenter的这个方法
     *
     * @param savedInstanceState 保存了的状态
     */
    void onUICreate(Bundle savedInstanceState);

    /**
     * onUIStart:在UI被创建和被显示到屏幕之间应该回调这个方法. <br/>
     * <p/>
     * 比如Activity的onStart()方法应该调用Presenter的这个方法
     */
    void onUIStart();

    /**
     * onUIResume:在UI被显示到屏幕的时候应该回调这个方法. <br/>
     * <p/>
     * 比如Activity的onResume()方法应该调用Presenter的这个方法
     */
    void onUIResume();

    /**
     * onUIPause:在UI从屏幕上消失的时候应该回调这个方法. <br/>
     * <p/>
     * 比如Activity的onPause()方法应该调用Presenter的这个方法
     */
    void onUIPause();

    /**
     * onUIStop:在UI从屏幕完全隐藏应该回调这个方法. <br/>
     * <p/>
     * 比如Activity的onStop()方法应该调用Presenter的这个方法
     */
    void onUIStop();

    /**
     * onUIDestroy:当UI被Destory的时候应该回调这个方法. <br/>
     */
    void onUIDestroy();

    /**
     * onSaveInstanceState:保存数据. <br/>
     * <p/>
     * 一般是因为内存不足UI的状态被回收的时候调用
     *
     * @param outState 待保存的状态
     */
    void onSaveInstanceState(Bundle outState);

    /**
     * onRestoreInstanceState:当UI被恢复的时候被调用. <br/>
     *
     * @param savedInstanceState 保存了的状态
     */
    void onRestoreInstanceState(Bundle savedInstanceState);
```
**封装BaseActivity**
拥有一个 protected P mPresenter实例，类型写成泛型，protected修饰，子类实现
   构造方法中，对mPresenter进行实例化：采用反射的形式（避免让子类进行实例化，繁琐）
```
public abstract class BaseMVPActivity<P extends IPresenter> extends BaseActivity {

  protected P mPresenter;
    public BaseMVPActivity(){
        this.mPresenter = createPresenter();
    }
  protected P createPresenter(){
        ParameterizedType type = (ParameterizedType)(getClass().getGenericSuperclass());
        if(type == null){
            return null;
        }
        Type[] typeArray = type.getActualTypeArguments();
        if(typeArray.length == 0){
            return null;
        }
        Class<P> clazz = (Class<P>) typeArray[0];
        try {
            return clazz.newInstance();
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        } catch (InstantiationException e) {
            e.printStackTrace();
        }
        return null;
    }

 @Override
    protected void onDestroy() {
        mPresenter.onUIDestroy();
        super.onDestroy();
    }
```
**封装BasePresenter**
3.定义BasePresenter，页面销毁的回调里面。处理网络请求
  定义一个集合，把每次网络请求装载到集合里面，在页面销毁的时候，取消所有的网络请求。防止内存泄漏。
```
public abstract class BasePresenter<U extends IUI> implements IPresenter {

 @Override
    public void onUIDestroy() {
        // 清空Call列表，并放弃Call请求
        clearAndCancelCallList();

    }
}
```


####  3.MVVM及其优缺点



View层包含布局,以及布局生命周期控制器(Activity/Fragment)

ViewModel与Presenter大致相同,都是负责处理数据和实现业务逻辑,但 ViewModel层不应该直接或者间接地持有View层的任何引用

model层是数据层


Model，模型层，即数据模型，用于获取和存储数据。

View，视图，即Activity/Fragment

ViewModel，视图模型，负责业务逻辑。



MVVM 的本质是 数据驱动，把解耦做的更彻底，viewModel不持有view 。

View 产生事件，使用 ViewModel进行逻辑处理后，通知Model更新数据，Model把更新的数据给ViewModel，ViewModel自动通知View更新界面，而不是主动调用View的方法

LiveData是具有生命周期的可观察的数据持有类。理解它需要注意这几个关键字，生命周期，可观察，数据持有类。

 DataBinding用来实现View层与ViewModel数据的双向绑定，Data Binding 減輕原本 MVP 中 Presenter 要與 p 和 View 互動的職責

MVVM的优点

核心思想是观察者模式,它通过事件和转移View层数据持有权来实现View层与ViewModel层的解耦.

1.耦合度更低，复用性更强，没有内存泄漏

2.结合jetpack，写出更优雅的代码

缺点

ViewModel与View层的通信变得更加困难了,所以在一些极其简单的页面中请酌情使用,否则就会有一种脱裤子放屁的感觉,在使用MVP这个道理也依然适用.



-----------------------------------------------------------------------------







####  4.MVC与MVP区别

View与Model并不直接交互，而是通过与Presenter交互来与Model间接交互。而在MVC中View可以与Model直接交互。MVP 隔离了MVC中的 M 与 V 的直接联系后，靠 Presenter 来中转，所以使用 MVP 时 P 是直接调用 View 的接口来实现对视图的操作的，

####  5.MVP如何管理Presenter的生命周期，何时取消网络请求

https://blog.csdn.net/mq2553299/article/details/78927617

https://www.jianshu.com/p/0d07fba84cb8

 使用RxLifecycle，通过监听Activity、Fragment的生命周期，来自动断开subscription以防止内存泄漏。

RxLifecycle原理

**操作符**

1.takeUntil 发射来自原始Observable的数据，如果第二个Observable发射了一项数据或者发射了一个终止通知， 原始Observable会停止发射并终止。

2.CombineLatest 当两个Observables中的任何一个发射了数据时，使用一个函数结合每个Observable发射的最近数据项，并且基于这个函数的结果发射数据。


**流程**

1.BehaviorSubject 在ActivityActivity不同的生命周期，BehaviorSubject对象会发射对应的ActivityEvent，比如在onCreate()生命周期发射ActivityEvent.CREATE，在onStop()发射ActivityEvent.STOP。

BehaviorSubject，实际上也还是一个Observable

BehaviorSubject （释放订阅前最后一个数据和订阅后接收到的所有数据）


2.LifecycleTransformer 在自己的请求中bindActivity返回的是LifecycleTransformer

 LifecycleTransformer中使用upstream.takeUntil(observable)，

upstream就是原始的Observable

observable是Activity中的BehaviorSubject

**指定生命周期断开**

原始的Observable通过takeUntil和BehaviorSubject绑定，当BehaviorSubject发出数据即Activity的生命周期走到和你指定销毁的事件一样时,BehaviorSubject才会把事件传递出去,原始的Observable就终止发射数据了

**不指定生命周期断开**

combineLatest() 当两个Observables中的任何一个发射了数据时，使用一个函数结合每个Observable发射的最近数据项，并且基于这个函数的结果发射数据。不指定生命周期时bindToLifecycle中通过combineLatest组合


比如说我们在onCreate()中执行了bindToLifecycle，那么lifecycle.take(1)指的就是ActivityEvent.CREATE，经过map(correspondingEvents)，这个map中传的函数就是 1中的ACTIVITY_LIFECYCLE

lifecycle.skip(1)就简单了，除去第一个保留剩下的，以ActivityEvent.Create为例，这里就剩下：ActivityEvent.START
ActivityEvent.RESUME
ActivityEvent.PAUSE
ActivityEvent.STOP
ActivityEvent.DESTROY


三个参数 意味着，lifecycle.take(1).map(correspondingEvents)的序列和 lifecycle.skip(1)进行combine，形成一个新的序列：

false,false,fasle,false,true

这意味着，当Activity走到onStart生命周期时，为false,这次订阅不会取消，直到onDestroy，为true，订阅取消。

最终还是和lifecycle（BehaviorSubject）发射的数据比较，如果两个一样说明Activity走到了该断开的生命周期了，upstream.takeUntil(observable)中的observable就要发通知告诉upstream（原始的Observable）该断开了。


