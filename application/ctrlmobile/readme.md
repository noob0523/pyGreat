### 安装SDK驱动
https://developer.android.com/studio/releases/platform-tools

配置环境变量，可以在命令行执行adb命令

### 华为手机打开开发者选项
1/3. 分步阅读 首先，打开手机中的设置，再点击系统。
2/3. 如果手机中的开发人员选项没有被隐藏，直接点击即可
3/3. 如果在系统中没有出现开发人员选项，那么点击关于手机，再多次点击版本号，大约七八下左右。 接下来会出现一行小字，您已处于开发者模式，无需进行此操作。 此时开发人员选项已打开。
### 打开手机调试模式
系统 =》操作人员选项 =》USB调试

### 查看IP
无线和网络 =》WLAN =》WLAN设置 =》IP地址

### 安装Android驱动
设备驱动状态正常。
这一点在 Linux 和 Mac OS X 下基本不用操心，在 Windows 下有可能遇到需要安装驱动的情况，确认这一点可以右键「计算机」-「属性」，
到「设备管理器」里查看相关设备上是否有黄色感叹号或问号，如果没有就说明驱动状态已经好了。否则可以下载一个手机助手类程序来安装驱动先。

### 手机端
手机端装起来比较习麻烦，最终从谷歌商店下载了一个，还是从一个Aptoide的软件中下的
选择‘仅充电’是不行滴(可以在开发人员选项中进行设置）；选择传文件是可以滴；

有线连接可以了
无线连接还有问题，被积极拒绝了
- 解决方式一（失败）

  首先得是用usb线成功连接了手机的
  
  adb shell   # 进入手机的shell模式
  ```cmd
  HWSCM:/ $ setprop service.adb.tcp.port 5555
  //设置adb服务端口为5555， 打开adb网络调试功能
  HWSCM:/ $ setprop service.adb.tcp.port -1 //表示打开adb的usb调试功能。 
  HWSCM:/ $ exit
  ```

- 方式二（失败）
  ```cmd
  adb usb   # 切换到usb模式
  adb kill-server
  adb tcpip 5555    # 切换到无线
  adb connect 192.168.0.1x:5555
  adb disconnect 192.168.0.1x   # 断开设备连接
  ```
  
- 三
  断开有线之后USB调试会被关闭，但是启动起来之后也并不能无线连接
  断开USB连接之后“USB调试”会被自动关闭，开启“仅充电模式下允许ADB调试”可以在断开连接后同时开启USB调试
  https://blog.csdn.net/H_O_W_E/article/details/88049760
