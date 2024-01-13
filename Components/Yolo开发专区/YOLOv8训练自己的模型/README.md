文档更新于2024-1-13  
作者:Teng
# 一、项目介绍
YOLOv8在windows11上的部署教程已出，本篇文档在[部署教程](https://github.com/twy2020/YAU-ICR/blob/main/Components/Yolo%E5%BC%80%E5%8F%91%E4%B8%93%E5%8C%BA/Win11%2BPycharm%E9%83%A8%E7%BD%B2YOLOv8/README.md)的基础上进行YOLOv8模型训练的教学
____
# 二、操作步骤
## Step 1: 制作标注数据集
### 1. 安装目标检测标注工具[Labelimg](https://zhuanlan.zhihu.com/p/550021453)
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
### 2. 标注
   - 采集一定数量的图片样本，图片数量开始时，可以准备100张左右（教程使用了97张）
   - 图片尺寸不宜过大，建议使用正方形640*640分辨率
   - 图片中应包含待训练识别的物体，可以有多个类别，多个数目的物体，考虑到图片数量一定，建议每张图片内包含重复物体的不同形态，视角，光影下的图像，丰富信息量
   - 在Labelimg界面中进行如下设置
     
     1) 勾选自动保存：view -> Auto Save Mode
     2) 勾选显示标签：view -> Display Labels
   - 创建一个文件夹，用来存放图片和标注数据，将图片拷贝至文件夹内（转化为png格式，方便后续划分数据集的脚本操作）
   - Labelimg中打开图像文件夹，选择数据也存放至此文件夹内
   - 按 W 键创建选区，框选物体并输入标签，A 和 D 键控制上一张下一张图片切换
   - 标注完成后，文件夹内应该存在与 .png 一一对应的 .txt 文件和 classes.txt 文件
   - 完成后关闭Labelimg
## Step 2: 开始训练
### 1. 划分数据集
   - 打开 Pycharm Community Edition
   - 打开 YOLOv8 项目目录，进入 `/ultralytics-main`
   - 在此目录下新建目录 `/datasets`
   - 进入 `/datasets`
   - 在此目录下新建目录 `/data`
   - 进入 `/data`
   - 在此目录下新建目录`/images`
   - 将刚才标注完成后的文件夹内所有文件拷贝至 `/images` 内
   - 回到 `/datasets` 目录下
   - 创建以下文件
     
     `mydata.yaml`
     ```yaml
     train: ./data/train/images
     val: ./data/val/images
     test: ./data/test/images
      
     # 类别数，打开刚刚的 classes.txt 文件，看里面有几行标签，这里就改成几
     nc: 4 
      
     # 类别名称，在 classes.txt 文件内按顺序添加标签的名称，不能改变顺序
     names: ['Label_1','Label_2','Label_3','Label_4']
     ```

     `Process.py`
     ```python
     import os
     import random
     import shutil

     def split_dataset(data_dir,train_val_test_dir, train_ratio, val_ratio, test_ratio):
        # 创建目标文件夹
        train_dir = os.path.join(train_val_test_dir, 'train')
        val_dir = os.path.join(train_val_test_dir, 'val')
        test_dir = os.path.join(train_val_test_dir, 'test')
        os.makedirs(train_dir, exist_ok=True)
        os.makedirs(val_dir, exist_ok=True)
        os.makedirs(test_dir, exist_ok=True)

     # 获取数据集中的所有文件
     files = os.listdir(data_dir)

     # 过滤掉非图片文件
     image_files = [f for f in files if f.endswith('.jpg') or f.endswith('.png')]
     # 随机打乱文件列表
     random.shuffle(image_files)

     # 计算切分数据集的索引
     num_files = len(image_files)
     num_train = int(num_files * train_ratio)
     num_val = int(num_files * val_ratio)
     num_test = num_files - num_train - num_val

     # 分离训练集
     train_files = image_files[:num_train]
     for file in train_files:
         src_image_path = os.path.join(data_dir, file)
         src_label_path = os.path.join(data_dir, file.replace('.jpg', '.txt').replace('.png', '.txt'))
         dst_image_path = os.path.join(train_dir, file)
         dst_label_path = os.path.join(train_dir, file.replace('.jpg', '.txt').replace('.png', '.txt'))
         shutil.copy(src_image_path, dst_image_path)
         shutil.copy(src_label_path, dst_label_path)

     # 分离验证集
     val_files = image_files[num_train:num_train+num_val]
     for file in val_files:
         src_image_path = os.path.join(data_dir, file)
         src_label_path = os.path.join(data_dir, file.replace('.jpg', '.txt').replace('.png', '.txt'))
         dst_image_path = os.path.join(val_dir, file)
         dst_label_path = os.path.join(val_dir, file.replace('.jpg', '.txt').replace('.png', '.txt'))
         shutil.copy(src_image_path, dst_image_path)
         shutil.copy(src_label_path, dst_label_path)

     # 分离测试集
     test_files = image_files[num_train+num_val:]
     for file in test_files:
         src_image_path = os.path.join(data_dir, file)
         src_label_path = os.path.join(data_dir, file.replace('.jpg', '.txt').replace('.png', '.txt'))
         dst_image_path = os.path.join(test_dir, file)
         dst_label_path = os.path.join(test_dir, file.replace('.jpg', '.txt').replace('.png', '.txt'))
         shutil.copy(src_image_path, dst_image_path)
         shutil.copy(src_label_path, dst_label_path)

     print("数据集分离完成！")
     print(f"训练集数量：{len(train_files)}")
     print(f"验证集数量：{len(val_files)}")
     print(f"测试集数量：{len(test_files)}")

     def move_files(data_dir):
         # 创建目标文件夹
         images_dir = os.path.join(data_dir, 'images')
         labels_dir = os.path.join(data_dir, 'labels')
         os.makedirs(images_dir, exist_ok=True)
         os.makedirs(labels_dir, exist_ok=True)

     # 获取数据集中的所有文件
     files = os.listdir(data_dir)
 
     # 移动PNG文件到images文件夹
     png_files = [f for f in files if f.endswith('.png')]
     for file in png_files:
         src_path = os.path.join(data_dir, file)
         dst_path = os.path.join(images_dir, file)
         shutil.move(src_path, dst_path)

     # 移动TXT文件到labels文件夹
     txt_files = [f for f in files if f.endswith('.txt')]
     for file in txt_files:
         src_path = os.path.join(data_dir, file)
         dst_path = os.path.join(labels_dir, file)
         shutil.move(src_path, dst_path)

     print(f"{data_dir}文件移动完成！")
     print(f"总共移动了 {len(png_files)} 个PNG文件到images文件夹")
     print(f"总共移动了 {len(txt_files)} 个TXT文件到labels文件夹")


     # 设置数据集路径和切分比例
     data_dir = 'data/images'  # 图片和标签路径
     train_val_test_dir= 'data'  # 目标文件夹
     train_ratio = 0.7               # 训练集比例
     val_ratio = 0.2                 # 验证集比例
     test_ratio = 0.1                # 测试集比例
      
     # 调用函数分离数据集
     split_dataset(data_dir, train_val_test_dir,train_ratio, val_ratio, test_ratio)
     # 调用函数移动文件
     move_files(os.path.join(train_val_test_dir, 'train'))
     move_files(os.path.join(train_val_test_dir, 'val'))
     move_files(os.path.join(train_val_test_dir, 'test'))
     ```

     `train.py`
     ```python
     from ultralytics import YOLO

     # Load a model
     #model = YOLO('yolov8n.yaml')  # build a new model from YAML
     model = YOLO('../../yolov8n.pt')  # load a pretrained model (recommended for training)
     #model = YOLO('yolov8n.yaml').load('yolov8n.pt')  # build from YAML and transfer weights
   
     if __name__ == '__main__':

     # Train the model
     model.train(data='./mydata.yaml', epochs=100, imgsz=640)
     ```
   - 先运行 `Process.py` 程序划分数据集，报错请按照提示检查数据集是否有问题，文件是否一一对应
### 开始训练
   - 记得修改 `mydata.yaml` 中的标签参数
   - 准备就绪，运行 `train.py` 开始训练
     
## Step 3: 检验效果
   - epochs为迭代次数，当前设置为100，100轮后即完成，最优模型存放在 `datasets/runs/trainx/weight/best.pt` （trainx一般选择最大数值）
   - 再拍摄一组待识别物体的照片用于查看效果
   - 打开 pycharm 终端，更改并输入以下命令进行测试
     
     ``
____
# 三、踩坑
