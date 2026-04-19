# 基于卷积神经网络的SVHN街景门牌数字识别对比研究

**课程：** 神经网络及其应用  
**学院：** 微电子学院  
**学号：** BC25219017  
**作者：** 宋城啸  
**日期：** 2026.4.19

---

## 摘要

本项目基于 [SVHN（Street View House Numbers）Format 2](http://ufldl.stanford.edu/housenumbers/) 数据集，在统一训练策略与评估协议下，设计并系统对比了三种卷积神经网络架构：

- **BasicCNN**：无批归一化的基础卷积网络，作为性能基线
- **ImprovedCNN**：在 BasicCNN 基础上引入批归一化与分级 Dropout 正则化
- **ResNetSVHN**：采用预激活残差结构与全局平均池化的轻量残差网络

实验结果表明，仅含约 272K 参数的 ResNetSVHN 在测试准确率与泛化能力上均超越参数量约为其 5 倍的 ImprovedCNN，验证了**"架构设计优于参数堆叠"**这一核心结论。

**关键词**：SVHN；卷积神经网络；残差网络；数据增强；对比实验

---

## 数据集

| 属性 | 详情 |
|------|------|
| 数据集来源 | SVHN Format 2（Google 街景） |
| 图像尺寸 | 32 × 32 像素，RGB 三通道 |
| 分类任务 | 10 类（数字 0–9） |
| 训练集规模 | 73,257 张 |
| 测试集规模 | 26,032 张 |
| 类别不均衡性 | 类别1最多（约13,861张），类别9最少（约4,659张） |

数据集可从 [Stanford SVHN 官网](http://ufldl.stanford.edu/housenumbers/) 下载（Format 2）。

---

## 项目结构

```
.
└── SVHN_CNN_Classification.ipynb   # 主实验 Notebook（数据加载、模型定义、训练与评估）
```

---

## 环境依赖

- Python 3.x
- PyTorch
- torchvision
- NumPy
- SciPy
- Matplotlib
- Seaborn
- scikit-learn
- Pillow

安装依赖：

```bash
pip install torch torchvision numpy scipy matplotlib seaborn scikit-learn pillow
```

---

## 实验流程

1. 加载 SVHN `.mat` 格式数据，基于训练集统计量完成归一化，9:1 划分训练/验证集
2. 设计数字识别任务专用数据增强策略（排除可能改变数字语义的翻转操作）
3. 实现 BasicCNN、ImprovedCNN 与 ResNetSVHN 三种架构并统计参数规模
4. 在统一超参数配置（优化器、学习率调度、早停策略）下训练三个模型
5. 通过训练曲线、混淆矩阵、类别准确率及错误样本分析完成系统性评估
6. 汇总结果，与公开基准对比，提出后续改进方向

---

## 主要结论

- **残差结构**（ResNetSVHN）以更少的参数量取得了最高的测试准确率，展现出更强的泛化能力
- **批归一化** 和 **Dropout 正则化** 能有效缓解过拟合，加快收敛
- 类别不均衡对少数类（如类别 9）的识别精度存在一定影响，可通过加权损失或过采样进一步改善

---

## 使用方法

1. 下载 SVHN Format 2 数据集（`train_32x32.mat` 和 `test_32x32.mat`），放置于 Notebook 中指定的数据目录
2. 打开并逐单元格运行 `SVHN_CNN_Classification.ipynb`
3. 训练完成后可在 Notebook 末尾查看各模型的性能对比图表与评估报告
