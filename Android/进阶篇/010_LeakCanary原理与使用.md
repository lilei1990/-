#####引入依赖
    //2.0以后已经不需要注册安装了
    dependencies {
      // debugImplementation because LeakCanary should only run in debug builds.
      debugImplementation 'com.squareup.leakcanary:leakcanary-android:2.4'
    }



#####模拟一个内存泄露
    public class MainActivity extends AppCompatActivity {
        private static final String TAG = "MainActivity";
        Handler handler = new Handler(){
            @Override
            public void dispatchMessage(Message msg) {
                super.dispatchMessage(msg);
                //do something
            }
        };
    
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            handler.sendEmptyMessageDelayed(0,60 * 1000);
        }
    }


#####原理概述
关于LeakCanary的原理，官网上已经给出了详细的解释。翻译过来就是：1.LeakCanary使用ObjectWatcher来监控Android的生命周期。当Activity和Fragment被destroy以后，这些引用被传给ObjectWatcher以WeakReference的形式引用着。如果gc完5秒钟以后这些引用还没有被清除掉，那就是内存泄露了。2.当被泄露掉的对象达到一个阈值，LeakCanary就会把java的堆栈信息dump到.hprof文件中。3.LeakCanary用Shark库来解析.hprof文件，找到无法被清理的引用的引用栈，然后再根据对Android系统的知识来判定是哪个实例导致的泄露。4.通过泄露信息，LeakCanary会将一条完整的引用链缩减到一个小的引用链，其余的因为这个小的引用链导致的泄露链都会被聚合在一起。

通过官网的介绍，我们很容易就抓住了学习LeakCanary这个库的重点：

LeakCanary是如何使用ObjectWatcher 监控生命周期的？
LeakCanary如何dump和分析.hprof文件的？
