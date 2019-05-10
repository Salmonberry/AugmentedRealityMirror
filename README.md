# AR魔镜开发进度概述

## 硬件设备

Intel® RealSense™ Depth 400系列

- Intel® RealSense™ Depth Camera D435

  - 同款对比

    与同期生产的同款深度摄像机D415相比，其镜头广度范围更广。

  - 原理 

    其原理是基于三角测量法，左右红外相机进行测量深度，中间红外点阵投射器相当于补光灯，不打开也能测深度，只是效果不好；最右边的RGB相机用于采集彩色图片，最终可以将彩色视频流与深度流进行对齐。

    ![](https://raw.githubusercontent.com/Salmonberry/ImgResource/master/Animation/20181030153126852.png)
    
  - RealSense SDk2.0 版本安装,请查阅[《RealSenseD435接入Nuitrack SDK》](./DOC/RealSense D435接入Nuitrack SDK.md)的**安装与检测部分**，Intel的开源Github仓库[intelRealSense/librealsense](https://github.com/IntelRealSense/librealsense)的**Download and Install**部分。
  
  - 文档与资料主要参考官方的[文档站点](<https://dev.intelrealsense.com/docs/>)和Intel的Github仓库中的[WiKi部分](<https://github.com/IntelRealSense/librealsense/wiki>)
  
  - [unity环境引入RealSense配置](<https://github.com/IntelRealSense/librealsense/tree/development/wrappers/unity>) 
  
  - [固件更新方法](./DOC/RealSense固件更新.md)
  
- Intel’s RealSense Tracking Camera T265 

  [官方宣称T265 能够提供3D localization for AR headsets and drones](<https://www.ithome.com/0/407/180.htm>).

  > Intel says the T265 is designed to work with, rather than replace, its existing RealSense D400 series off cameras. The [RealSense Depth Camera D435i](https://www.slashgear.com/intel-realsense-d435i-stereo-depth-camera-revealed-6dof-now-a-reality-13553544/) announced last November, for instance, brings motion and gesture detection, rotational tracking, stabilization, and orientation tracking. Combined with the T265, they could achieve occupancy mapping, improved 3D scanning, and advanced navigation and collision avoidance.
  >
  > The RealSense Tracking Camera T265 requires a USB 2.0 or USB 3.0 connection (with at least 1.5W of power) and hardware with enough non-volatile memory to boot the camera. It’s available for preorder, priced at $199, and Intel says it expects to begin shipping from February 28.


## 存在问题
 RealSense SDk2.0中的Unity中去除了人物的体感识别和脸部识别的集成模块Demo,官方也没有更多的资料可供参考。而采用C++或C#开发,调用相关模块，难度会相对的困难（比较适合有图形学openCV开发基础的人使用）

# 备选方案（第三方SDK）

 在使用Realsense D435的基础上，接入第三方SDK：**Nuitrack SDK**

![](https://raw.githubusercontent.com/Salmonberry/ImgResource/master/Animation/Nuitrack.png)

### 接入方式

- [RealSense D435接入Nuitrack SDK](./DOC/RealSense D435接入Nuitrack SDK.md)

###  Nuitrack资料

- [官网SDK下载](<https://nuitrack.com/>)
- [文档](<http://download.3divi.com/Nuitrack/doc/>)
- [论坛](<https://community.nuitrack.com/>):可以向管理员请教问题，一般第二天就会给答复（应该是时差的问题）
- [windons 下的Nuitrackde 环境配置](http://download.3divi.com/Nuitrack/doc/Installation_page.html)

- Unity项目中引入NuitrackSDK.unitypackage

  - 官网首页下载NuitrackSDK包
  - 解压压缩包，路径：NuitrackSDK>Unity3D>**NuitrackSDK.unitypackage**，双击**NuitrackSDK.unitypackage**导入包到工程中。
  - Unity项目中，路径：**Assets>Tutorials>FaceTracker>FinalAssets**中，双击**FaceTracking**场景文件打开场景，点击**Run**运行，即可查看效果

### FaceTracking的各模块逻辑调用关系

![](https://raw.githubusercontent.com/Salmonberry/ImgResource/master/Animation/Nuitrack_First%20Project.png)

具体代码块功能解析，请按照模块逻辑调用关系顺序，在**src>FaceTrack.unitypackage**中查看**RGB>Scripts**中的代码注释。