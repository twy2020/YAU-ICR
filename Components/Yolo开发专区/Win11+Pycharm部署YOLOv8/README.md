文档更新于2024-1-12  
作者:Teng
____
# 一、文档介绍
本文档根据作者的实践经验和网上众多教程，分享YOLOv8的快速部署方法
____
# 二、配置参考
- 操作系统:Windows11
- 编译器:Pycharm Community Edition 2022.2.2
- Anaconda版本:conda 23.7.2(终端查看版本指令:conda --version)
- python版本:python=3.8(YOLOv8要求python >= 3.8)
- 运行内存:16g
- 显卡:LapTop RTX3060 6GB
____
# 三、步骤
## Step1 python环境准备(建议开启魔法)
### 1、安装Anaconda
- 官网下载地址: [https://www.anaconda.com/download](https://www.anaconda.com/download)
- 下载完毕后请安装到自定义位置
### 2、创建python环境
- windows搜索并打开Anaconda Prompt命令窗口
- 输入命令创建环境"pytorch"(可选路径，可选python版本，可选环境名)
 
  `conda create --prefix=C:/ProgramData/Anaconda3/envs/pytorch python=3.8`
- 选择y开始创建
- 输入命令查看环境
  
  `conda env list`
- 复制环境路径(C:/ProgramData/Anaconda3/envs/pytorch)
- 输入命令进入环境
  
  `conda activate C:/ProgramData/Anaconda3/envs/pytorch`
- 提示符前面括号变为(pytorch)即成功进入环境
  
  ![image](https://github.com/twy2020/YAU-ICR/blob/main/Components/Yolo%E5%BC%80%E5%8F%91%E4%B8%93%E5%8C%BA/Win11%2BPycharm%E9%83%A8%E7%BD%B2YOLOv8/pic/Snipaste_2024-01-12_03-34-09.png)
## Step2 在环境内安装pytorch(针对Nivdia GPU)
### 1、确定显卡和驱动是否满足要求
- 输入命令查看显卡信息和驱动版本
  
  `nvidia-smi`
- 找到如图信息
  
  ![image](https://github.com/twy2020/YAU-ICR/blob/main/Components/Yolo%E5%BC%80%E5%8F%91%E4%B8%93%E5%8C%BA/Win11%2BPycharm%E9%83%A8%E7%BD%B2YOLOv8/pic/Snipaste_2024-01-12_03-32-03.png)
- 对照下表确定是否满足要求
### 2、安装pytorch
- 进入pytorch官网: [https://pytorch.org/](https://pytorch.org/)
- 选择 python,pip,你的cuda版本
- 复制生成的指令
- 回到终端，粘贴指令，回车执行
- 等待自动安装完成
### 3、检验pytorch安装情况
- 输入指令进入python解释器
  
  `python`
- 输入代码
  
  ```python
  import torch
  ```
- 无错误返回为正常
- 输入代码检查cuda是否正常
  
  ```python
  torch.cuda.is_available()
  ```
- 返回True即可，返回False需要检查前面的pytorch安装步骤，版本是否正确，cuda版本是否满足要求等，建议删除环境重装
## Step3 下载utralytics(YOLOv8项目)
### 1、从github下载原项目代码
- utralytics项目地址: [https://github.com/ultralytics/ultralytics](https://github.com/ultralytics/ultralytics)
### 2、使用pycharm开发项目
- 将项目解压至指定路径
- pycharm 打开项目
- 选择python解释器为你创建的Anaconda环境路径，应识别到python.exe
### 3、安装依赖
- pycharm内打开内置终端，输入指令
  
  `pip install utralytics`
- 等待完成
## Step4 测试YOLOv8
- 终端输入指令测试YOLOv8
  
  `yolo task=detect mode=predict  model=yolov8n.pt conf=0.25 source='ultralytics/assets/bus.jpg'`
____
