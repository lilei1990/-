# Flutter 入门

- Android Studio 安装
  - **安装Flutter和Dart插件**
    - **需要安装两个插件**:
        - Flutter插件： 支持Flutter开发工作流 (运行、调试、热重载等).
        - Dart插件： 提供代码分析 (输入代码时进行验证、代码补全等).
    - **run**
      - 启动Android Studio.
      - 打开插件首选项 (Preferences>Plugins on macOS, File>Settings>Plugins on
        Windows & Linux).
      - 选择 Browse repositories…,
      - 选择 Flutter 插件并点击 install. 重启Android Studio后插件生效.

    - **创建新应用**
      - 选择 File>New Flutter Project
      - 选择 Flutter application 作为 project 类型, 然后点击 Next
      - 输入项目名称 (如 myapp), 然后点击 Next
      - 点击 Finish
      - 等待Android Studio安装SDK并创建项目.

        ` 如果第一次创建项目需要下载SDK,会超级慢,可以参考镜像自己`
        [手动下载](https://mirrors.tuna.tsinghua.edu.cn/flutter/flutter_infra/releases/stable/)`创建项目的时候会下载一些库卡死,或者配置下面环境变量镜像`

            //环境变量
            PUB_HOSTED_URL=https://pub.flutter-io.cn
            FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn
            //克隆sdk
            git clone -b dev https://github.com/flutter/flutter.git


