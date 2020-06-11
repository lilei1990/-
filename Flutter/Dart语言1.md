＃-学习笔记

- 1.变量声明

  - var:可以接收任何类型的变量，var变量一旦赋值，类型便会确定，则不能再改变其类型，

              var t;
              t = "hi world";
              // 下面代码在dart中会报错，因为变量t的类型已经确定为String，
              // 类型一旦确定后则不能再更改其类型。
              t = 1000;
  - dynamic和Object
    - Object 是Dart所有对象的根基类(包括Function和Null)，dynamic与var一样都是关键词,声明的变量可以赋值任意对象。
               而dynamic与Object相同之处在于,他们声明的变量可以在后期改变赋值类型。
    - dynamic与Object不同的是,dynamic声明的对象编译器会提供所有可能的组合, 而Object声明的对象只能使用Object的属性与方法

                   dynamic a;
                   Object b;
                   main() {
                       a = "";
                       b = "";
                       printLengths();
                   }   
                  
                   printLengths() {
                       // no warning
                       print(a.length);
                       // warning:
                       // The getter 'length' is not defined for the class 'Object'
                       print(b.length);
                   }
  - final和const
    - 一个 final 变量只能被设置一次
    - const 变量是一个编译时常量
    - final变量在第一次使用时被初始化。
    - 被final或者const修饰的变量，变量类型可以省略

- 2.函数
  - 函数声明

        bool isNoble(int atomicNumber) {
          return _nobleGases[atomicNumber] != null;
        }       
  - Dart函数声明如果没有显式声明返回值类型时会默认当做dynamic处理，注意，函数返回值没有类型推断：

          typedef bool CALLBACK();
        
        //不指定返回类型，此时默认为dynamic，不是bool
        isNoble(int atomicNumber) {
          return _nobleGases[atomicNumber] != null;
        }
        
        void test(CALLBACK cb){
           print(cb()); 
        }
        //报错，isNoble不是bool类型
        test(isNoble);
  - 对于只包含一个表达式的函数，可以使用简写语法

        bool isNoble (int atomicNumber)=> _nobleGases [ atomicNumber ] ！= null ;
  - 函数作为变量

        var say = (str){
          print(str);
        };
        say("hi world");
  - 函数作为参数传递

        void execute(var callback) {
            callback();
        }
        execute(() => print("xxx")) 
  - 可选的位置参数

        //包装一组函数参数，用[]标记为可选的位置参数，并放在参数列表的最后面：
        String say(String from, String msg, [String device]) {
          var result = '$from says $msg';
          if (device != null) {
            result = '$result with a $device';
          }
          return result;
        }
        //调用
        say('Bob', 'Howdy'); //结果是： Bob says Howdy
        say('Bob', 'Howdy', 'smoke signal'); //结果是：Bob says Howdy with a smoke signal
  - 可选的命名参数

        //定义函数时，使用{param1, param2, …}，放在参数列表的最后面，用于指定命名参数。例如：      
        //设置[bold]和[hidden]标志
        void enableFlags({bool bold, bool hidden}) {
            // ... 
        }
        //调用函数时，可以使用指定命名参数。例如：paramName: value
        enableFlags(bold: true, hidden: false);