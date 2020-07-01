##### Android开发的四大组件
- Activity
- Service
- ContentProvider
- BroadcastReceive

##### startService 和 bindService 特点
- 启动方式：Context.startService

- 启动方式：Context.bindService 

- 停止方式：Context.stopService 或者 Service.stopSelf

- 停止方式：Context.unbindService

- 多次启动只会多次执行 onStartCommand 方法，只要调用一次 stopService 服务就会销毁

- 多次启动 onBind  一般只执行一次（特殊情况可以多次执行），当所有绑定者都与service 解绑时，service 会自行销毁，其中单独某一个绑定者解绑，service 不会销毁

- 生命周期：onCreate --> onStartCommand --> onDestory

- 生命周期：onCreate --> onBind--> onUnbind--> onDestory

- 服务启动后执行单一的操作并且不会向调用者返回结果，无法通信

- 服务启动后允许组件与服务进行交互、发送请求、获取结果，甚至是利用进程间通信 (IPC) 跨进程执行这些操作

- 调用者退出后，Service 仍然存在

- 调用者退出后，Service（只有一个绑定者时） 随着调用者销毁

- 启动一次服务，多次调用 stopService 只有第一次有效，不会抛出异常

- 启动一次服务，多次调用 unbindService 会抛出异常（IllegalArgumentException：Service not registered）
注意：

>不论哪种方式启动服务，onCreate 只会执行一次，只有当服务销毁（onDestory）后再次启动服务时，又会重新调用 onCreate

>Service与Activity一样都存在于当前进程的主线程，所以，一些阻塞UI的操作，比如耗时操作不能放在service里进行

>bindService 启动服务，绑定者在销毁（onDestory）前需要先解绑，
否则出 *** has leaked ServiceConnection 等错误日志，
意思就是服务连接泄露（因为在关闭Acitivity的时候没有释放链接），
这个错误就好像我们启动了一个对话框，此时我们没有关闭对话框，
如果直接关闭了启动对话框的Activity，也会出现类似的错误，
这个时候我们只需要在Acitivity销毁时释放链接就可以了
##### **五种布局**

全都继承自ViewGroup，各自特点及绘制效率对比。

- -FrameLayout 框架布局

	
> 此布局是五种布局中最简单的布局，Android中并没有对child view的摆布进行控制，
> 这个布局中所有的控件都会默认出现在视图的左上角，我们可以使用android:layout_margin，android:layout_gravity等属性去控制子控件相对布局的位置。

- -LinearLayout 线性布局

 
>  一行（或一列）只控制一个控件的线性布局，所以当有很多控件需要在一个界面中列出时，
>  可以用LinearLayout布局。 此布局有一个需要格外注意的属性:android:orientation=“horizontal|vertical。


- -AbsoluteLayout 绝对布局

> 可以放置多个控件，并且可以自己定义控件的x,y位置

- -RelativeLayout 相对布局

> 这个布局也是相对自由的布局，Android 对该布局的child view的 水平layout& 垂直layout做了解析，
> 由此我们可以FrameLayout的基础上使用标签或者Java代码对垂直方向 以及 水平方向 布局中的views进行任意的控制



- -TableLayout 表格布局

> 将子元素的位置分配到行或列中，一个TableLayout由许多的TableRow组成


- -GridLayout网格布局 

> 作为android 4.0 后新增的一个布局,与前面介绍过的TableLayout(表格布局)其实有点大同小异;
> 不过新增了一些东东
> 
> ①跟LinearLayout(线性布局)一样,他可以设置容器中组件的对齐方式
> 
> ②容器中的组件可以跨多行也可以跨多列(相比TableLayout直接放组件,占一行相比较)

- -ConstraintLayout约束布局

> 约束布局ConstraintLayout 是一个ViewGroup，可以在Api9以上的Android系统使用它，
> 它的出现主要是为了解决布局嵌套过多的问题，以灵活的方式定位和调整小部件。
> 从 Android Studio 2.3 起，官方的模板默认使用 ConstraintLayout

