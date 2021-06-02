

## interface IDroneApi 
用于访问无人机属性的接口
####Bundle getAttribute(String attributeType);
        /**
        * 检索其类型由参数指定的属性。
        * @param attributeType要检索的属性的类型。支持的列表
          类型存储在{@link com.o3dr.services.android.lib.drone.attribute.AttributeType}中。
        * @return Bundle 对象包含请求的属性。
          */

####void performAction(inout Action action);
              /**
          * 在 api 公开的集合中执行一个操作。
          * @param action 要执行的操作。
          */
  ##/ ***单向方法调用*** /

####oneway void performAsyncAction(in Action action);
          /**
      * 在 api 公开的集合中异步执行一个操作。
      * @param action 要执行的操作。
      */

####oneway void addAttributesObserver(IObserver observer);
      /**
    *注册一个侦听器以接收无人机事件。
    * @paramobserver 要注册的观察者。
      */

####oneway void removeAttributesObserver(IObserver observer);
        
        /**
        *删除无人机事件监听器。
        * @paramobserver 要移除的观察者。
        */

####oneway void addMavlinkObserver(IMavlinkObserver observer);
          /**
      * 注册一个监听器来接收 mavlink 消息。
      * @paramobserver 要注册的观察者。
      */

####oneway void removeMavlinkObserver(IMavlinkObserver observer);
          /**
      * 删除一个 mavlink 消息监听器。
      * @paramobserver 要移除的观察者。
      */

####void executeAction(inout Action action, ICommandListener listener);
          /**
      * 在 api 公开的集合中执行一个操作。
      * @param action 要执行的操作。
      */
/ ***单向方法调用*** /


####oneway void executeAsyncAction(in Action action, ICommandListener listener);
          /**
      * 在 api 公开的集合中异步执行一个操作。
      * @param action 要执行的操作。
      * @param侦听器注册在执行操作时要调用的回调。
      */