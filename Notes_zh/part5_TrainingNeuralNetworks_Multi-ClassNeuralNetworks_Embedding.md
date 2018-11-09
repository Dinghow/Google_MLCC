### 14. 训练神经网络

最常见的神经网络训练算法：[反向传播算法](https://google-developers.gonglchuangl.net/machine-learning/crash-course/backprop-scroll/)（BP算法，BackPropagation）

> 是一种与[最优化方法](https://zh.wikipedia.org/wiki/%E6%9C%80%E4%BC%98%E5%8C%96)（如[梯度下降法](https://zh.wikipedia.org/wiki/%E6%A2%AF%E5%BA%A6%E4%B8%8B%E9%99%8D%E6%B3%95)）结合使用的，用来训练[人工神经网络](https://zh.wikipedia.org/wiki/%E4%BA%BA%E5%B7%A5%E7%A5%9E%E7%BB%8F%E7%BD%91%E7%BB%9C)的常见方法。该方法对网络中所有权重计算[损失函数](https://zh.wikipedia.org/w/index.php?title=%E6%8D%9F%E5%A4%B1%E5%87%BD%E6%95%B0&action=edit&redlink=1)的梯度。这个梯度会反馈给最优化方法，用来更新权值以最小化损失函数。

很多情况都会导致BP算法出错

- 梯度消失：较低层（更接近输入）的梯度可能会变得非常小。在深度网络中，计算这些梯度时，可能涉及许多小项的乘积。当较低层的梯度逐渐消失到 0 时，这些层的训练速度会非常缓慢，甚至不再训练。

  ReLU 激活函数有助于防止梯度消失。

- 梯度爆炸：如果网络中的权重过大，则较低层的梯度会涉及许多大项的乘积。在这种情况下，梯度就会爆炸：梯度过大导致难以收敛。

  批标准化可以降低学习速率，因而有助于防止梯度爆炸。

- ReLu单元消失：一旦 ReLU 单元的加权和低于 0，ReLU 单元就可能会停滞，梯度无法反向传播。由于梯度的来源被切断，ReLU 的输入可能无法作出足够的改变来使加权和恢复到 0 以上。

  降低学习速率有助于防止 ReLU 单元消失。



丢弃正则化

> 一种形式的[**正则化**](https://developers.google.cn/machine-learning/crash-course/glossary#regularization)，在训练[**神经网络**](https://developers.google.cn/machine-learning/crash-course/glossary#neural_network)方面非常有用。丢弃正则化的运作机制是，在神经网络层的一个梯度步长中移除随机选择的固定数量的单元。丢弃的单元越多，正则化效果就越强。



### 15. 多类别神经网络

#### 一对多

一对多提供了一种利用二元分类的方法，对于N个可行的解决方案，就包括N个单独的二元分类器

![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/google-10.png)

#### Softmax

> Softmax函数，又称为归一化函数，它能将一个含任意实数的K维向量 $Z$ “压缩”到另一个K维实向量 $\sigma(z)$中，使得每一个元素的范围都在之间$(0,1)$，并且所有元素的和为1。

根据Softmax函数的这一特点，常常将其用多类别领域，Softmax为每个类别分配一个小数表示概率，其和为1

Softmax函数的表达式为：

![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/18.png)

而在神经网络中，Softmax层必须有和输出层一样的节点数

#### Softmax的选项

- 完整Softmax：针对所有类别都要计算概率
- 候选采样：针对正类别标签计算概率，针对负类别标签随机采样计算概率

> **候选采样：**在训练一个多类别分类器过程中，所有的类别都需要进行评估。为了解决这个问题，人们发明了候选采样的技巧，每次只评估所有类别的一个很小的子集。tensorflow包含了多种候选采样函数

#### Softmax不适用的情况

对于每一个样本可能是多个类别的成员是，Softmax不适用，必须依赖于多个逻辑回归



### 16. 嵌入(Embedding)

#### 定义

> 一种分类特征，以连续值特征表示。通常，嵌入是指将高维度向量映射到低维度的空间。可以理解为数据降维，在数学上即表示一个mapping,f:X->Y，而Y的维度低于X。
>
> 例如，您可以采用以下两种方式之一来表示英文句子中的单词：
>
> - 表示成包含百万个元素（高维度）的[**稀疏向量**](https://developers.google.cn/machine-learning/glossary/#sparse_features)，其中所有元素都是整数。向量中的每个单元格都表示一个单独的英文单词，单元格中的值表示相应单词在句子中出现的次数。由于单个英文句子包含的单词不太可能超过 50 个，因此向量中几乎每个单元格都包含 0。少数非 0 的单元格中将包含一个非常小的整数（通常为 1），该整数表示相应单词在句子中出现的次数。
> - 表示成包含数百个元素（低维度）的[**密集向量**](https://developers.google.cn/machine-learning/glossary/#dense_feature)，其中每个元素都存储一个介于 0 到 1 之间的浮点值。这就是一种嵌套。

#### 适用

使用独热编码表示法时，产生的输入矢量可能会比较稀疏，会使得训练的数据量和计算量变得十分庞大，且矢量之间缺乏有意义的联系，在这种情况下，使用嵌套对数据进行降维可以很好地解决这个问题

#### 训练

可以将嵌入作为目标任务的神经网络的一部分进行学习。如图所示，嵌入单元实际上就是大小为d（采用d维嵌套，即可以通过d维的矢量在d维空间下表示出一个样本）的一个特殊类型的隐藏单元。嵌入层只是一个隐藏层，无需单独的训练过程，像之前一样通过反向传播即可进行训练。

![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/google-11.png)