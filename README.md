# AI图搜图应用开发（DINOv2 + Flask）
本仓库是「Python程序设计」课程中，基于DINOv2模型的AI图搜图应用开发实验代码实现。


## 实验简介
基于DINOv2视觉Transformer模型，实现了**图片特征提取、百万级特征库构建、余弦相似度检索**三大核心功能，并完成Web端可视化检索界面的开发。其中`build_index.py`、`app.py`、`retrieval.py`分别对应特征库构建、Web服务启动、检索逻辑实现三大核心任务。


## 环境依赖
需安装以下Python库：
```bash
# 安装依赖
pip install numpy==1.26.4 flask==2.3.3 pillow==10.2.0

1. 如何验证模型正确性
- 准备完整的`dinov2_numpy.py`实现
- 运行`validate_model.py`进行快速测试
- 对比输出：将提取的特征与参考文件（`./test_data/standard_feature.npz`）比较，确保误差在0.01以内的可接受范围

2. 特征库批量构建
- 下载10,000+公开图片数据集（`dataset.csv`）作为基础图库
- 用`preprocess_image.py`实现“短边缩放”：将不同分辨率图片统一缩放到短边224px，且尺寸需为14的整数倍
- 通过自定义ViT（`dinov2_numpy.py`）提取所有图库图片的768维特征
- 存储特征：将特征矩阵与图片标签映射关系保存至`gallery_features.npz`，支持断点续传

3. 在线检索流程
- 用户上传图片时，先通过`preprocess_image.py`完成预处理
- 调用`dinov2_numpy.py`提取上传图片的特征向量
- 计算相似度：用余弦相似度算法对比上传图片特征与图库特征库
- 返回结果：按相似度降序排序，取前10个结果并返回对应图片路径与相似度值
- .
