#Flow 基本使用
方法一:flow builder

     flow {
             for (i in 1..5) {
                 delay(300)
                 emit(i)
             }
         }.map {
             it * it
         }.flowOn(Dispatchers.IO)
             .collect {
                 println(it)
             }
方法二: flowOf() 帮助可变数组生成 Flow 实例,调用的就是第一种flow{}

      flowOf(1, 2, 3, 4, 5)
            .onEach {
                delay(100)
            }
            .collect {
                println(it)
            }
方法三: asFlow() 面向数组、列表等集合

      listOf(1, 2, 3, 4, 5).asFlow()
              .onEach {
                  delay(100)
              }.collect {
                  println(it)
              }
方法三: channelFlow()
     
     channelFlow {
            for (i in 1..5) {
                delay(100)
                send(i)
            }
        }.collect{
            println(it)
        }
      
>collect 方法和 RxJava 中的 subscribe 方法一样，都是用来消费数据的。

>collect 函数是一个 suspend 方法，所以它必须发生在协程或者带有 suspend 的方法里面，这也是我为什么在一开始的时候启动了

>lifecycleScope.launch。lifecycleScope 是我使用的 Lifecycle 的协程扩展库当中的，你可以替换成自定义的协程作用域

>flowOn(Dispatchers.IO)切换线程。

>emit发送值
 
 
##Flow操作符
**transform**

在使用transform操作符时，可以任意多次调用emit。

    runBlocking {
    
                    (1..5).asFlow()
                        .transform {
                            emit(it * 2)
                            delay(100)
                            emit(it * 4)
                        }
                        .collect { println("transform:$it") }
                }
    打印
    transform:2
    transform:4
    transform:4
    transform:8
    transform:6
    transform:12
    transform:8
    transform:16
    transform:10
    transform:20

**take**

take操作符只取前几个emit发射

      (1 .. 5).asFlow().take(2).collect {
                        println("take:$it")
                    }
    打印
    take:1
    take:2

**reduce**

简单点理解就是两个元素操作之后拿到的值跟后面的元素进行操作,用于把flow 简化合并为一个值。

      runBlocking {
                      val sum=( 1 ..5).asFlow()
                          .reduce { a, b ->
                              println("reduce:${a},${b}")
                              a*b
                          }
      
                       println(sum)
      
                  }
    打印
    reduce:1,2 
    reduce:2,3
    reduce:6,4
    reduce:24,5
    120

**fold**

end---我也不知道怎么解释,不懂看源码,凑合就这么理解吧 

      runBlocking {
         val sum = (1..5).asFlow()
             .map { it * it }//平方相乘
             .fold(1) { a, b -> a + b }//1是初始值
         println(sum)

      }

    打印 
    fold:1,1
    fold:2,4
    fold:6,9
    fold:15,16
    fold:31,25
    56
    
**zip**

zip可以将2个flow进行合并的操作符 flowA中的item个数大于flowB中的item个数，执行合并后新flow的item个数=较小的flow的item个数。

      fun main() = runBlocking {
      
          val flowA = (1..5).asFlow()
          val flowB = flowOf("one", "two", "three", "four", "five").onEach { delay(100) }
      
          val time = measureTimeMillis {
              flowA.zip(flowB) { a, b -> "$a and $b" }
                  .collect { println(it) }
          }
      
          println("Cost $time ms")
      }

    打印 
    1 and one
    2 and two
    3 and three
    4 and four
    5 and five
    Cost 540 ms

**flattenMerge/flattenConcat**

zip可以将2个flow进行合并的操作符 flowA中的item个数大于flowB中的item个数，执行合并后新flow的item个数=较小的flow的item个数。

      val flowA = (1..5).asFlow()
      val flowB = flowOf("one", "two", "three", "four", "five")
      
        flowOf(flowA,flowB).flattenMerge(2).collect {
                          println("flattenMerge:$it")
                      }
      
                      flowOf(flowA,flowB).flattenConcat().collect{println("flattenConcat:$it")}


    打印 
    flattenMerge:1
    flattenMerge:2
    flattenMerge:3
    flattenMerge:4
    flattenMerge:5
    flattenMerge:one
    flattenMerge:two
    flattenMerge:three
    flattenMerge:four
    flattenMerge:five
    
    flattenConcat:1
    flattenConcat:2
    flattenConcat:3
    flattenConcat:4
    flattenConcat:5
    flattenConcat:one
    flattenConcat:two
    flattenConcat:three
    flattenConcat:four
    flattenConcat:five
    
**flatMapConcat**

flatMapConcat由map,flattenMerge操作符联合完成。

      fun currTime() = System.currentTimeMillis()
      
                  var start: Long = 0
                  runBlocking {
      
                      (1..5).asFlow()
                          .onStart { start = currTime() }
                          .onEach { delay(100) }
                          .flatMapConcat {
                              flow {
                                  emit("$it: First")
                                  delay(500)
                                  emit("$it: Second")
                              }
                              
                          }
                          .collect {
                              println("$it at ${System.currentTimeMillis() - start} ms from start")
                          }
                  }


    打印 
    1: First at 124 ms from start
    1: Second at 625 ms from start
    2: First at 726 ms from start
    2: Second at 1228 ms from start
    3: First at 1328 ms from start
    3: Second at 1829 ms from start
    4: First at 1930 ms from start
    4: Second at 2431 ms from start
    5: First at 2532 ms from start
    5: Second at 3033 ms from start

**flatMapMerge**

并发收集flows并且将合并它们的值为一个单一flow，因此发射地值会尽快被处理。。

      fun requestFlow(i: Int): Flow<String> = flow {
          emit("$i: First") 
          delay(500) // wait 500 ms
          emit("$i: Second")    
      }
      
      fun main() = runBlocking<Unit> { 
          val startTime = System.currentTimeMillis() // remember the start time 
          (1..3).asFlow().onEach { delay(100) } // a number every 100 ms 
              .flatMapMerge { requestFlow(it) }                                                                           
              .collect { value -> // collect and print 
                  println("$value at ${System.currentTimeMillis() - startTime} ms from start") 
              } 
      }


    打印 
    1: First at 136 ms from start
    2: First at 231 ms from start
    3: First at 333 ms from start
    1: Second at 639 ms from start
    2: Second at 732 ms from start
    3: Second at 833 ms from start

**flatMapLatest**

flatMapLatest和collectLatest操作符很像，只有新flow发射了新值，那么上个flow就会被取消。

      fun requestFlow(i: Int): Flow<String> = flow {
          emit("$i: First") 
          delay(500) // wait 500 ms
          emit("$i: Second")    
      }
      
      fun main() = runBlocking<Unit> { 
          val startTime = System.currentTimeMillis() // remember the start time 
          (1..3).asFlow().onEach { delay(100) } // a number every 100 ms 
              .flatMapLatest { requestFlow(it) }                                                                           
              .collect { value -> // collect and print 
                  println("$value at ${System.currentTimeMillis() - startTime} ms from start") 
              } 
      }


    打印 
    1: First at 142 ms from start
    2: First at 322 ms from start
    3: First at 425 ms from start
    3: Second at 931 ms from start

            
         
**conflate**

当一个flow表示操作的部分结果或者操作状态更新，它可能并不需要取处理每一个值，但是需要处理最近的一个值。在这种场景下，
conflate操作符可以被用于忽略中间操作符。是一种对emit和collector慢处理的一种方式，它通过丢弃一些值来实现。


      fun foo(): Flow<Int> = flow {
          for (i in 1..3) {
              delay(100) // pretend we are asynchronously waiting 100 ms
              emit(i) // emit next value
          }
      }
      
      fun main() = runBlocking<Unit> { 
          val time = measureTimeMillis {
              foo()
                  .conflate() // conflate emissions, don't process each one
                  .collect { value -> 
                      delay(300) // pretend we are processing it for 300 ms
                      println(value) 
                  } 
          }   
          println("Collected in $time ms")
      }


    打印 
    1
    3
    Collected in 758 ms

            
            
            


