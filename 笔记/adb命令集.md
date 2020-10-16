# adb链接mumu模拟器
    adb connect 127.0.0.1:7555
    adb shell
# adb所有设备
    adb devices
# adb指定序列号，进入
	adb -s d51ad9ff shell
# adb设置手机连接端口号
	adb tcpip 8888
	设置成功
	restarting in TCP mode port: 8888

# adb查看网络连接
	adb shell netstat

    -r  Display routing table.
    -a  Display all sockets (Default: Connected).
    -l  Display listening server sockets.
    -t  Display TCP sockets.
    -u  Display UDP sockets.
    -w  Display Raw sockets.
    -x  Display Unix sockets.
    -e  Display other/more information.
    -n  Don't resolve names.
    -W  Wide Display.
    -p  Display PID/Program name for sockets.
    
# adb查看进程
adb shell-->ps -A |grep lifecycle
# adb杀死进程
adb shell-->am kill com.example.android.codelabs.lifecycle

