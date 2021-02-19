######### 查看构建版本
    gradlew -v
##### 清除build文件夹
    gradlew clean
##### 检查依赖并编译打包
    gradlew build
##### 编译并安装debug包
    gradlew installDebug
##### 编译并打印日志
    gradlew build --info
##### 译并输出性能报告，性能报告一般在 构建工程根目录 build/reports/profile
    gradlew build --profile
##### 调试模式构建并打印堆栈日志
    gradlew build --info --debug --stacktrace
##### 强制更新最新依赖，清除构建并构建
    gradlew clean build --refresh-dependencies
#####  XXX表示想打印的module的name
    gradlew XXX:dependencies
#####  打release包
    gradlew assembleRelease
#####  打印依赖
    gradlew :app:dependencies
#####  安装
    gradlew installDebug
