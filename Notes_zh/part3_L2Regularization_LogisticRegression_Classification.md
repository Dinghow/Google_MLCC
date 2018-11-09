### 9.正则化(Regularization)：简单性

#### L2正则化

定义：通过降低复杂模型的复杂度来**防止过拟合**的原则称为正则化

为了避免训练集数据过拟合，应该求**结构风险最小化**（最小化损失和复杂度）：

![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/2.png)

![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/google-4.png)

而衡量模型复杂度有两种常见方式：

- 用所有特征的权重的函数

  可以使用 **L2 正则化**公式来量化复杂度，该公式将正则化项定义为所有特征权重的平方和：

  ![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/3.png)

- 用具有非零权重的特征总数的函数



执行L2正则化对模型的影响：

- 使权重接近于0（并非正好为0）
- 使权重的平均值接近于0，且呈正态（钟形曲线或高斯曲线）分布

> L2 正则化降低较大权重的程度高于降低较小权重的程度。因此，即使某个权重降低的速度比另一个快，L2 正则化也往往会使较大权重降低的速度快于较小的权重。

#### Lambda

lambda又称**正则化率**

模型开发者通过以下方式来调整正则化项的整体影响：用正则化项的值乘以名为 **lambda**的标量

即：

![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/4.png)

增加lambda值将增强正则化的效果（直方图更剧烈），降低lambda值则会得到比较平缓的直方图

理想的 lambda 值取决于数据，因此您需要手动或自动进行一些调整



### 10.逻辑回归 (Logistic Regression)

#### 定义

一种模型，通过将 [**S 型函数**](https://developers.google.cn/machine-learning/crash-course/glossary#sigmoid_function)应用于线性预测，生成分类问题中每个可能的离散标签值的概率（有渐近线，可以提供(0,1)之间的有界值）。虽然逻辑回归经常用于[**二元分类**](https://developers.google.cn/machine-learning/crash-course/glossary#binary_classification)问题，但也可用于[**多类别**](https://developers.google.cn/machine-learning/crash-course/glossary#multi-class)分类问题（其叫法变为**多类别逻辑回归**或**多项回归**）。

#### S型函数的运用

如果 z 表示使用逻辑回归训练的模型的线性层的输出，则 S 型(z) 函数会生成一个介于 0 和 1 之间的值（概率）。用数学方法表示为：

![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/5.png)

- y' 是逻辑回归模型针对特定样本的输出

- z 是 b + w1x1 + w2x2 + … wNxN，又称为对数几率，因为z的反函数为：

  ![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/6.png)

  - w:该模型学习的权重和偏差
  - x:特定样本的特征值

![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/google-5.png)

#### 损失函数

对数损失函数：

![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/7.png)

- (x,y)&straightepsilon;D 是包含很多有标签样本 (x,y) 的数据集。
- “y”是有标签样本中的标签。由于这是逻辑回归，因此“y”的每个值必须是 0 或 1。
- “y'”是对于特征集“x”的预测值（介于 0 和 1 之间）。

#### 逻辑回归中的正则化

因为逻辑回归的渐近性，如果不进行正则化，模型会因为促使所有样本的损失达到0但又做不到而造成过拟合，逻辑回归常常采用一下三种正则化方法：

- L1正则化
- L2正则化
- 早停法（即限制训练步数或步长）

### 11.分类

#### 真与假以及正类别与负类别

|                    | 正例（预测值） | 反例（预测值） |
| :----------------: | :------------: | :------------: |
| **正例（真实值）** |   真正例(TP)   |   假正例(FP)   |
| **反例（真实值）** |   假负例(FN)   |   真负例(TN)   |

正类别、负类别（Positive,Negative）：定义的样本中的二分类情况

真、假（True,False）:真——实际值与预测值相同，假——实际值与预测值相反

**真正例**是指模型将正类别样本正确地预测为正类别。同样，**真负例**是指模型将负类别样本正确地预测为负类别。

**假正例**是指模型将负类别样本错误地预测为正类别，而**假负例**是指模型将正类别样本错误地预测为负类别。

TP,TN不会造成损失

#### 准确率(Accuracy)

定义：预测正确的结果所占比例

![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/8.png)

二分类问题中

![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/9.png)

#### 精确率和召回率（Precision & Recall）

##### 精确率

定义：表示的是预测为正的样本中有多少是真正的正样本，又称为**查准率**

![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/10.png)

##### 召回率

定义：表示真正的正样本中有多少被正确预测，又称为**查全率**

![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/11.png)

查准和查全二者之间是矛盾的。查准率高（尽可能只挑选有把握的），那查全率就会低；查全率高（试想把所有类别都预测为正例），那查准率就会低。

为了综合考虑二者，常常采用$F_1$值：

![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/12.png)

#### ROC和曲线下面积

真正例率	(TPR)：等同于召回率

![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/13.png)

假正例率(FPR)：

![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/14.png)

ROC 曲线用于绘制采用不同分类阈值时的 TPR 与 FPR

#### ROC和曲线下面积

##### ROC曲线

真正例率(TPR)：等同于召回率

![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/15.png)

假正例率(FPR)：

![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/16.png)

ROC(Receiver Operating Characteristic Curve)曲线用于绘制采用不同分类阈值时的 TPR 与 FPR，横轴为FPR，纵轴为TPR

![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/google-6.png)

ROC曲线的主要作用：

- 能很容易的查出任意阈值对学习器的泛化性能影响 
- 有助于选择最佳的阈值。ROC曲线越靠近左上角，模型的查全率就越高。最靠近左上角的ROC曲线上的点是分类错误最少的最好阈值，其假正例和假反例总数最少 
- 可以对不同的学习器比较性能。将各个学习器的ROC曲线绘制到同一坐标中，直观地鉴别优劣，靠近左上角的ROC曲所代表的学习器准确性最高 

##### AUC

ROC曲线下面积(Area Under ROC Curve)用来反映分类器对**样本的排序能力**，取值范围[0.5,1s]一般情况下AUC越大模型较佳

> AUC就是从所有1样本中随机选取一个样本, 从所有0样本中随机选取一个样本,然后根据你的分类器对两个随机样本进行预测，把1样本预测为1的概率为p1，把0样本预测为1的概率为p0，p1>p0的概率就是AUC

改善AUC的一种方法：只要不过拟合，就训练更长时间——增加步数/或批量大小



#### 预测偏差

预测偏差  =  预测平均值 - 数据集中相应标签的平均值

造成预测偏差的原因可能有：

1. 特征集不完整
2. 数据集混乱
3. 模型实现的流水线有错误
4. 训练样本有偏差
5. 正则化过强

可以通过校准层来纠正预测偏差，但是使用校准层需注意：

- 校准层仅仅是修复症状而非原因
- 相当于建立了一个更脆弱的系统，需要持续地更新

因此并不推荐使用校准层。

逻辑回归常常用于预测0/1值，所以无法根据一个样本就确定预测偏差，需要运用分桶的方法在每个桶中计算预测偏差