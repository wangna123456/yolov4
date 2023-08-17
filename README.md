# yolov4    Win10+vs2019+opencv+darknet进行目标检测

1、环境配置

1.1 CMake

版本>=3.18，下载：https://cmake.org/download/

我下载的是最新版本3.27.1

安装后需要配置环境，找到cmake的路径
![image](https://github.com/wangna123456/yolov4/assets/142497906/f86c7968-727f-4c1e-a243-c7a65c4dd625)

添加到系统变量

![image](https://github.com/wangna123456/yolov4/assets/142497906/c5d675cc-5a2b-4765-bbd8-a0c3c55ab658)

到cmake目录下执行cmd命令cmake -version检查cmake是否配置成功，出现cmake版本表示配置成功。
![image](https://github.com/wangna123456/yolov4/assets/142497906/193218db-7b81-48d8-aca7-3182770e6245)


1.2 CUDA

版本>=10.2: https://developer.nvidia.com/cuda-toolkit-archive 

我这里下载了11.1.1，这个要看安装的显卡最高支持到的CUDA版本（最好先安装显卡最新驱动程序，并在NVIDIA控制面版里查看），并不是最新就http://wed.xjx100.cn/news/157710.html?action=onClick

CUDA的三个文件分别放在以下几个目录中
![image](https://github.com/wangna123456/yolov4/assets/142497906/27d4e2ad-ff16-4827-a164-61e0c1dfaec0)


安装后配置环境变量
计算机上点右键，打开属性->高级系统设置->环境变量，可以看到系统中多了CUDA_PATH和 CUDA_PATH_V11_1两个环境变量

![image](https://github.com/wangna123456/yolov4/assets/142497906/e04c5ae7-119b-4ff9-a006-c86bef541834)

接下来，还要在系统中添加以下几个环境变量:

![image](https://github.com/wangna123456/yolov4/assets/142497906/1b3c5979-d7e1-40b9-a3f8-4eb028815905)

然后，在系统变量 Path 的末尾添加：
再添加如下5条：

![image](https://github.com/wangna123456/yolov4/assets/142497906/f825722e-f38a-44f6-9910-853b16be1e40)

CUDA测试——CMD执行nvcc -V：（如果没有反应，就重启一下电脑）

出现下图所示界面表示配置成功。

![image](https://github.com/wangna123456/yolov4/assets/142497906/cfb98b6c-c93d-4804-9add-e1a37dbddb18)

2.3 cuDNN

版本>= 8.0.2，https://developer.nvidia.com/rdp/cudnn-archive

这个版本要与CUDA版本对应，我下载的是8.9.3.

cuDNN下载好后直接将其解开压缩包，然后需要将bin,include,lib中的文件分别复制粘贴到CUDA相对应的文件夹下

![image](https://github.com/wangna123456/yolov4/assets/142497906/62348084-55ec-4f3d-95ab-68da7b414e42)

检查是否配置成功

Win+R打开命令行窗口

进入CUDA安装目录下的子目录：extras\demo_suit\，如F:\YOLOV4\CUDA\CUDA Development\extras\demo_suite

依次输入.\bandwidthTest.exe，.\deviceQuery.exe测试

若键入命令之后，可得到类似下图结果，则说明配置成功。
![image](https://github.com/wangna123456/yolov4/assets/142497906/47bf0c94-922f-4e66-998d-ee41ca901565)

![image](https://github.com/wangna123456/yolov4/assets/142497906/a26eff18-3750-49a5-8bb7-bb72b2a67636)


2.4 OpenCV

版本>= 2.4: https://github.com/opencv/opencv_contrib/releases

安装完后要在系统变量中添加：OPENCV_DIR=F:\YOLOV4\opencv\build（按实际OPENCV所在路径直到build）

![image](https://github.com/wangna123456/yolov4/assets/142497906/050a69fd-a758-474a-915f-faad030b13fe)

在系统变量 Path 的末尾添加：F:\YOLOV4\opencv\build\x64\vc16\bin

![image](https://github.com/wangna123456/yolov4/assets/142497906/be4a413b-d310-4d9f-8a33-d957971e57bf)

2.5 MSVC

安装VS2019
![image](https://github.com/wangna123456/yolov4/assets/142497906/4a60a1b4-e3af-4cc0-8d41-c95d23aef6b3)

2.配置YOLOv4环境

2.1 官网下载YOLOV4代码 https://github.com/AlexeyAB/darknet

![image](https://github.com/wangna123456/yolov4/assets/142497906/afc8dbc6-b622-4eae-8d5a-8711e56dbb61)

保存到本地

![image](https://github.com/wangna123456/yolov4/assets/142497906/645b547a-1413-4420-b8f0-97ac64aa0c28)

2.2 复制OpenCV文件到darknet_master

将文件夹F:\YOLOV4\opencv\build\x64\vc16\bin的两个dll文件： opencv_ﬀmpeg480_64.dll和opencv_world480.dll复制到D:\darknet\build\darknet\x64 

![image](https://github.com/wangna123456/yolov4/assets/142497906/47225f73-da21-4728-b86a-ce4c28c3581e)

2.3 VS2019项目配置

首先通过Cmake_GUI 编译并打开darknet_master项目
![image](https://github.com/wangna123456/yolov4/assets/142497906/2073c0ed-2d53-4724-932a-1e8065f58a47)

Configure中选择V2019，x64

![image](https://github.com/wangna123456/yolov4/assets/142497906/5c246cd4-7ba8-4eac-bccb-105a561d669d)

在初次编译的时候，因为缺少zlibwapi.dll文件，出现报错，解决办法:从网上找到相应的文件，将zlibwapi.dll，zlibwapi.lib分别放到如下目录下即可。

![image](https://github.com/wangna123456/yolov4/assets/142497906/bc29d6aa-dfec-4dbe-a550-0112d2fcaf1c)


下图编译成功，没有报错

![image](https://github.com/wangna123456/yolov4/assets/142497906/d89d8a77-b50d-4580-a263-05824c0ffec8)

接下来配置VS2019

1.选择release和x64

![image](https://github.com/wangna123456/yolov4/assets/142497906/5f1e82b7-0dd0-4a7f-a028-addb5c16eef7)

2.项目 ->属性 注意同样应选release和x64，同时检查注意检查Windows SDK版本和平台工具集

![image](https://github.com/wangna123456/yolov4/assets/142497906/42ad8687-7269-46ce-89c0-b3d8dda297bb)

3.修改包含目录和库目录

添加opencv3.4的包含目录和库目录（按照自己的opencv3.4的路径

