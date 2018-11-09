## 机器学习概念

### 1.机器学习术语

#### 常见术语

- 标签：预测的事物，y变量
- 特征：输入变量，x变量
- 样本：特定实例，**x**
  - 有标签样本
  - 无标签样本
- 模型：定义了x与y之间的关系

- 监督学习（根据输入数据及其对应的[**标签**](https://developers.google.cn/machine-learning/glossary/#label)来训练[**模型**](https://developers.google.cn/machine-learning/glossary/#model)）：
  - 分类：离散值（好坏）
  - 回归：连续值（价格）

- 无监督学习（训练[**模型**](https://developers.google.cn/machine-learning/glossary/#model)，以找出数据集（通常是无标签数据集）中的规律）：
  - 聚类
- 参数：机器学习系统自行训练的模型的变量（如权重）
- 超参数：在模型训练的连续过程中，训练者可以调节的变量（如学习速率）

- 数值概念
  - 单个数值(Scalar)
  - 一维数组/矢量(Vector)
  - 二维数组(Matrix)
  - 三维以上(Tensor)



### 2.深入了解机器学习

#### 训练与损失：

##### 损失 (Loss)

一种衡量指标，用于衡量模型的[**预测**](https://developers.google.cn/machine-learning/crash-course/glossary#prediction)偏离其[**标签**](https://developers.google.cn/machine-learning/crash-course/glossary#label)的程度。或者更悲观地说是衡量模型有多差。要确定此值，模型必须定义损失函数。例如，线性回归模型通常将[**均方误差**](https://developers.google.cn/machine-learning/crash-course/glossary#MSE)用于损失函数，而逻辑回归模型则使用[**对数损失函数**](https://developers.google.cn/machine-learning/crash-course/glossary#Log_Loss)。

均方误差（MSE）：

![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/1.png)

### 3.降低损失

在求解机器学习算法的模型参数，即无约束优化问题时，梯度下降（Gradient Descent）是最常采用的方法之一，另一种常用的方法是最小二乘法。在求解损失函数的最小值时，可以通过梯度下降法来一步步的迭代求解，得到最小化的损失函数和模型参数值。

 梯度下降算法中，下一点位置 = 梯度x学习速率（步长）

> **梯度(gradient)**：[**偏导数**](https://developers.google.cn/machine-learning/glossary/#partial_derivative)相对于所有自变量的向量。 在机器学习中，梯度是模型函数偏导数的向量。梯度指向最快上升的方向。
>
> **梯度下降法(gradient descent)**：一种通过计算并且减小梯度将[**损失**](https://developers.google.cn/machine-learning/glossary/#loss)降至最低的技术，它以训练数据为条件，来计算损失相对于模型参数的梯度。通俗来说，梯度下降法以迭代方式调整参数，逐渐找到[**权重**](https://developers.google.cn/machine-learning/glossary/#weight)和偏差的最佳组合，从而将损失降至最低。
>
> **梯度下降法的几个基本概念**
>
> - batchsize：每批数据量的大小，DL通常用SGD（随机梯度下降）的优化算法进行训练，也就是一次（1 个iteration）一起训练batchsize个样本，计算它们的平均损失函数值，来更新参数
> - iteration：1个iteration即迭代一次，也就是用batchsize个样本训练一次
> - epoch（时期）：1个epoch表示过了1遍训练集中的所有样本，如定义10000次迭代为1个epoch，若每次迭代的batchsize设为256，那么1个epoch相当于过了2560000个训练样本
>
> (period:只是用来动态显示损失度量)

#### 迭代方法

![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/google-1.jpg)

### 4.使用TF基础

合成特征：一种[**特征**](https://developers.google.cn/machine-learning/crash-course/glossary#feature)，不在输入特征之列，而是从一个或多个输入特征衍生而来

