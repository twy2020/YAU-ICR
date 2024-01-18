# 手把手带你入门树莓派
文档修改于2024-1-15  
作者:Teng
____
# 一、文档简介
本文档分享作者在树莓派开发起步做的一些准备工作和遇到的坑，适用于想使用树莓派进行开发的新手，文档仅供参考
# 二、开发环境
- 科学上网
- PC端系统：Windows 11
- 树莓派系统：ubuntu-22.04-LTS-Desktop(如果想要使用ros2，此版本支持ros2的最新版本且系统5年内保持更新，稳定可靠)
- 树莓派版本：Raspberry-Pi 4b
# 三、制作系统卡
   - 准备一张 32GB 以上的 TF 卡，一个 TF 卡读卡器
     
![image](https://github.com/twy2020/YAU-ICR/blob/main/Components/Raspberry-Pi%E4%B8%93%E5%8C%BA/%E6%A0%91%E8%8E%93%E6%B4%BE%E5%85%A5%E9%97%A8%E7%BB%8F%E9%AA%8C/pic/2b92b660bb10f880483a706c3562591.jpg)
   - 下载 SD Card Formatter 工具对 TF 卡进行格式化
     
     官网:[https://www.sdcardformatter.com/start-download/?id=1](https://www.sdcardformatter.com/start-download/?id=1)

     解压并安装，打开

     将 TF 卡插入读卡器，将读卡器插入电脑

     找到你的卡的盘符，确认卡内没有重要文件后，可以更改盘符名称，点击 Format 格式化

![image](https://github.com/twy2020/YAU-ICR/blob/main/Components/Raspberry-Pi%E4%B8%93%E5%8C%BA/%E6%A0%91%E8%8E%93%E6%B4%BE%E5%85%A5%E9%97%A8%E7%BB%8F%E9%AA%8C/pic/Snipaste_2024-01-18_12-49-04.png)
   - 下载树莓派官方镜像烧录工具 Raspberry Pi Imager
     
     官网:[https://www.raspberrypi.com/software/](https://www.raspberrypi.com/software/)
     
![image](https://github.com/twy2020/YAU-ICR/blob/main/Components/Raspberry-Pi%E4%B8%93%E5%8C%BA/%E6%A0%91%E8%8E%93%E6%B4%BE%E5%85%A5%E9%97%A8%E7%BB%8F%E9%AA%8C/pic/Snipaste_2024-01-18_12-59-03.png)  

   安装并打开  
     选择其他系统，选择 ubuntu-22.04-LTS-Desktop 镜像，选择储存卡为刚刚格式化的卡，别着急烧录  
     
![image](https://github.com/twy2020/YAU-ICR/blob/main/Components/Raspberry-Pi%E4%B8%93%E5%8C%BA/%E6%A0%91%E8%8E%93%E6%B4%BE%E5%85%A5%E9%97%A8%E7%BB%8F%E9%AA%8C/pic/Snipaste_2024-01-18_14-10-06.png)        
     点击右下角的设置按钮，进行基础配置，否则后续无法方便地连接树莓派进行开发，设置好用户名和密码以及WIFI自动连接设置  

![image](https://github.com/twy2020/YAU-ICR/blob/main/Components/Raspberry-Pi%E4%B8%93%E5%8C%BA/%E6%A0%91%E8%8E%93%E6%B4%BE%E5%85%A5%E9%97%A8%E7%BB%8F%E9%AA%8C/pic/Snipaste_2024-01-18_13-19-15.png)  

  点击 烧录 -> 是，等待写入完成  
  设置热点，建议使用电脑开启热点(不要使用5G频段，部分树莓派没有5G天线，具体查阅说明书)，用 clash 的 allow lan 功能可以让树莓派进行科学上网  
  烧录完成，取下 TF 卡
# 四、树莓派，启动！
- 将系统卡插入树莓派卡槽
- 插入配套电源，注意稳定供电
  
   


     
