**五种布局**

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

**Activity生命周期。**
