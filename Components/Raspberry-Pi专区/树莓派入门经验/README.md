# 手把手带你入门树莓派
文档修改于2024-1-15  
作者:Teng
____
# 一、文档简介
本文档分享作者在树莓派开发起步做的一些准备工作和遇到的坑，适用于想使用树莓派进行开发的新手，文档仅供参考
# 二、开发环境
- PC端系统：Windows 11
- 树莓派系统：ubuntu-22.04-LTS-Desktop(如果想要使用ros2，此版本支持ros2的最新版本且系统5年内保持更新，稳定可靠)
- 树莓派版本：Rasspberry-Pi 4b
# 三、安装系统
1. 下载ubuntu-22.04-LTS-Desktop系统
   - ubuntu官网:[https://cn.ubuntu.com/download/alternative-downloads](https://cn.ubuntu.com/download/alternative-downloads)
     
![image](https://github.com/twy2020/YAU-ICR/blob/main/Components/Raspberry-Pi%E4%B8%93%E5%8C%BA/%E6%A0%91%E8%8E%93%E6%B4%BE%E5%85%A5%E9%97%A8%E7%BB%8F%E9%AA%8C/pic/Snipaste_2024-01-18_11-35-29.png)

![image](https://github.com/twy2020/YAU-ICR/blob/main/Components/Raspberry-Pi%E4%B8%93%E5%8C%BA/%E6%A0%91%E8%8E%93%E6%B4%BE%E5%85%A5%E9%97%A8%E7%BB%8F%E9%AA%8C/pic/Snipaste_2024-01-18_11-36-28.png)  


2. 制作系统卡
   - 准备一张 32GB 以上的 TF 卡，一个 TF 卡读卡器
     
![image](https://github.com/twy2020/YAU-ICR/blob/main/Components/Raspberry-Pi%E4%B8%93%E5%8C%BA/%E6%A0%91%E8%8E%93%E6%B4%BE%E5%85%A5%E9%97%A8%E7%BB%8F%E9%AA%8C/pic/2b92b660bb10f880483a706c3562591.jpg)  

   - 下载 SD Card Formatter 格式化工具
     
     官网:[https://www.sdcardformatter.com/start-download/?id=1](https://www.sdcardformatter.com/start-download/?id=1)

     解压并安装，打开

     将 TF 卡插入读卡器，将读卡器插入电脑

     找到你的卡的盘符，确认卡内没有重要文件后，可以更改盘符名称，点击 Format 格式化

![image](https://github.com/twy2020/YAU-ICR/blob/main/Components/Raspberry-Pi%E4%B8%93%E5%8C%BA/%E6%A0%91%E8%8E%93%E6%B4%BE%E5%85%A5%E9%97%A8%E7%BB%8F%E9%AA%8C/pic/Snipaste_2024-01-18_12-49-04.png)
