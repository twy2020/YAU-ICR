文档更新于2024-1-13  
作者:Teng
# 一、项目介绍
YOLOv8在windows11上的部署教程已出，本篇文档在[部署教程](https://github.com/twy2020/YAU-ICR/blob/main/Components/Yolo%E5%BC%80%E5%8F%91%E4%B8%93%E5%8C%BA/Win11%2BPycharm%E9%83%A8%E7%BD%B2YOLOv8/README.md)的基础上进行YOLOv8模型训练的教学
____
# 二、操作步骤
## Step 1: 制作标注数据集
1. 安装目标检测标注工具[Labelimg](https://zhuanlan.zhihu.com/p/550021453)
   - 在部署教程里已经完成了 python 3.8 环境的建立，可以继续在此环境中安装Labelimg
   - 打开 Anaconda prompt 终端
   - 输入指令查看环境列表
     
     `conda env list`
   - 输入指令切换到pytorch环境
     
     `conda activate 环境路径`
   - 输入指令安装依赖和Labelimg
     
     `pip install PyQt5`
     
     `pip install pyqt5-tools`
     
     `pip install lxml`
     
     `pip install labelimg`
   - 安装完成后输入指令启动Labelimg
     
     `Labelimg`
   - 注意：Lableimg要求 python <= 3.9 ，如果你之前的python环境大于此版本，可以考虑重新创建一个conda环境专门用来安装Labelimg（简单），或者参照[CSDN教程](https://blog.csdn.net/m0_74232237/article/details/130985914?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522169279443716800225569678%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=169279443716800225569678&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-1-130985914-null-null.142%5Ev93%5EchatgptT3_2&utm_term=labelimg%E9%97%AA%E9%80%80%20%20canvas.py&spm=1018.2226.3001.4187)
2. 标注
   - 采集一定数量的图片样本，图片数量开始时，可以准备100张左右（教程使用了97张）
   - 图片尺寸不宜过大，建议使用正方形640*640分辨率
   - 图片中应包含待训练识别的物体，可以有多个类别，多个数目的物体，考虑到图片数量一定，建议每张图片内包含重复物体的不同形态，视角，光影下的图像，丰富信息量
   - 在Labelimg界面中进行如下设置
     
     1) 勾选自动保存：view -> Auto Save Mode
     2) 
## Step 2: 开始训练
## Step 3: 检验效果
____
# 三、踩坑
