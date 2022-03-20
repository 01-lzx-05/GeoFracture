# GeoFracture

**1**、**代码仓库地址**
https://github.com/01-lzx-05/GeoFracture

**2**、**项目模块及完成情况**

（1）<u>山西可见光.tif处理（已完成，使用工具ArcGIS Pro）</u>

  --地裂缝标签标注：
  
  第一次在ArcGIS上标注，在ArcGIS Pro上使用时遇到问题：分类工具中标注对象以供深度学习使用加载训练样本时每个标签都被标注为新的一类，导致出现了900多类，尝试使用按ID字段转，输出像元大小跟图像一致，没有解决https://blog.csdn.net/qq_40357974/article/details/93744357
     
  第二次标注 ArcGIS pro标注对象以供深度学习使用，重来了一遍，麻了~，标注对象数量964
      
  --数据集制作：
  
   首先尝试使用python来对tif图片文件和shp标签同时进行裁剪，奈何图片过于大30多G，根本无法加载进，换为Matlab同样无法读入图片矩阵
    
   尝试利用mask掩膜首先对图片进行裁剪，分成四块，再对四个分块进行数据集制作，分别制作了左上数据集、右上数据集、左下数据集、右下数据集
   
   更新：发现ArcGIS Pro有制作数据集的功能，影像分析工具-->深度学习-->导出训练数据进行深度学习，图像格式jpeg/tif，tif的有点大，选择jpeg，元数据：PASCAL可视化对象用于目标检测，已分类切片用于像素分类，分别制作了两种格式的数据集。
   
   共3652张图片，切片大小256*256
   
（2）<u>目标检测（效果很差）</u>

  --yolov3：详细笔记见ipad GoodNotes的yolo

    测试./darknet detector test cfg/geogracture.data cfg/yolov3.cfg backup/yolov3_20000.weights data/0001.jpg -thresh 0.4

  --SSD:
    
    backbone:Resnet34；学习率：自动选择最佳
    
   效果很差，loss和currect图十分极端，只要有阴影的地方都会标记为地裂缝
  
  
（3）<u>像素分类</u>
  
  --U-net:
  
      backbone:Resnet34；学习率：自动选择最佳；二分类
      
      结果：较上面有很大提升，由于数据集标注不够精准，在结果中裂缝的标注范围偏大，需要修改数据集
  
  
**3**、**本周完成任务如下**
  
在训练和测试过程中发现自身对神经网络和深度学习的了解还不够透彻，无法对模型应用以自己的想法，开始学习之旅
  
（1）计算机视觉中的特征工程（3.13）
  
（2）图像分类网络模型框架（3.13）
 
 --vggnet：多卷积层串联结构，代码见classify中vggnet.py
 
 --resnet: 残差块基本单元包括主分支和跳连分支，out=out1+out2,，代码见classify中Resnet.py
 
 --mobilenetv1:轻量级，深度可分离卷积+住店卷积，代码见classify中mobilenetv1.py
 
 --inceptionMolule:并联网络，代码见classify中inceptionMolule.py
 
 （3）目标检测模型框架（3.20）
 
  mmdetection训练自己的数据集
 
 （4）像素分割模型框架（3.20）
 
  mmdectron框架训练自己的数据集
  
  （5）移植自己的图像分割框架（3.20）
  
  LZX-mmsegementation，具体代码见代码仓库
  
