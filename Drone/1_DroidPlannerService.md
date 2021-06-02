## DroidPlannerService

DroneKit-Android 后台服务实现。

     //状态栏通知id
      private static final int FOREGROUND_ID = 101;
    
      String CHANNEL_ID = "channel_id_01";
    
      String CHANNEL_NAME = "channel_hd_drone";

        //通知本地应用程序组件服务事件的一组操作。
      public static final String ACTION_DRONE_CREATED = Utils.PACKAGE_NAME + ".ACTION_DRONE_CREATED";
      public static final String ACTION_DRONE_DESTROYED = Utils.PACKAGE_NAME + ".ACTION_DRONE_DESTROYED";
      public static final String ACTION_RELEASE_API_INSTANCE = Utils.PACKAGE_NAME + ".action.RELEASE_API_INSTANCE";
      public static final String EXTRA_API_INSTANCE_APP_ID = "extra_api_instance_app_id";

        //用于广播服务事件
      private LocalBroadcastManager lbm;

        //存储每个连接的客户端的无人机api实例。客户端由其应用程序ID表示
      final ConcurrentHashMap<String, DroneApi> droneApiStore = new ConcurrentHashMap<>();

        //缓存每种连接类型的无人机管理器。
      final ConcurrentHashMap<ConnectionParameter, DroneManager> droneManagers = new ConcurrentHashMap<>();

      private DPServices dpServices;

      private CameraInfoLoader cameraInfoLoader;

      private List<CameraDetail> cachedCameraDetails;


#### DroneApi registerDroneApi(IApiListener listener, String appId)
    /**
      * 为给定应用程序 ID 表示的客户端生成一个无人机 API 实例。
      *
      * @param侦听器用于检索api信息。
      * @param appId连接客户端的应用程序ID。
      * @return 一个 IDroneApi 实例
      */

#### void releaseDroneApi(String appId)

          /**
      *释放附加到给定应用ID的无人机api实例。
      *
      * @param appId断开连接的客户端的应用程序ID。
      */


#### DroneManager connectDroneManager(ConnectionParameter connParams, String appId, DroneApi listener) 

    /**
    * 使用给定的连接参数与媒介建立连接。
    *
    * @param connParams用于连接到车辆的参数。
    * @param appId连接客户端的应用程序ID。
    * @param监听器回调以接收无人机事件。
    * @return 一个 DroneManager 实例，它充当连接车辆和监听客户端之间的路由器。
    */

#### void disconnectDroneManager(DroneManager droneMgr, DroneApi.ClientInfo clientInfo) 

    /**
    *从给定的无人机管理员管理的车辆上断开给定的客户。
    *
    * @paramdroneMgr 连接车辆的处理程序。
    * @param clientInfo断开连接的客户端的信息。
    */


#### synchronized List<CameraDetail> getCameraDetails() 
    
    /**
    * 检索应用程序提供的一组相机信息。
    *
    * @返回{@link CameraDetail}对象的列表。
    */


#### public IBinder onBind(Intent intent) 

    /**server bind 调用**/
 


#### public void onCreate() 

    /** 生命周期 **/

#### private void updateForegroundNotification()

    /** 通知栏显示更新 **/

#### public void onDestroy() 

#### public int onStartCommand(Intent intent, int flags, int startId)

    /** releaseDroneApi **/
#### public static void enableDroidPlannerService(Context context, boolean enable)

    /**
     * 关闭开启服务 DroidPlannerService 组件
     */
