### 12. 正则化：稀疏性

稀疏矢量的特征组合通常会导致包含更多无意义维度，在降低模型复杂度时，我们希望将一些无意义的权重设为0（即L0正则化），但是L0正则化是非凸优化，并存在其他问题，所以我们将条件放宽至L1正则化，减小权重的绝对值，即采用L1正则化

> 凸优化：不严格的说，凸优化就是在标准优化问题的范畴内，要求目标函数和约束函数是凸函数的一类优化问题。

#### L1正则化

##### L1 和 L2 正则化

L2 和 L1 采用不同的方式降低权重：

- L2 会降低权重2。
- L1 会降低 |权重|。

因此，L2 和 L1 具有不同的导数：

- L2 的导数为 2 * 权重。
- L1 的导数为 k（一个常数，其值与权重无关）

即

- L2正则化永远不回将权重变为0
- L1正则化可以使权重为0: L1 在 0 处具有不连续性，这会导致与 0 相交的减法结果变为 0。例如，如果减法使权重从 +0.1 变为 -0.2，L1 便会将权重设为 0



### 13. 神经网络

#### 基本概念

之前处理特殊的非线性问题时，我们采用了特征组合的方法，但是对于一般的非线性问题，我们采用神经网络来进行模型的建立。

> 神经网络(neural network)：一种模型，灵感来源于脑部结构，由多个层构成（至少有一个是[**隐藏层**](https://developers.google.cn/machine-learning/crash-course/glossary#hidden_layer)），每个层都包含简单相连的单元或[**神经元**](https://developers.google.cn/machine-learning/crash-course/glossary#neuron)（具有非线性关系）。
>
> 隐藏层(hidden layer)：[**神经网络**](https://developers.google.cn/machine-learning/crash-course/glossary#neural_network)中的合成层，介于[**输入层**](https://developers.google.cn/machine-learning/crash-course/glossary#input_layer)（即特征）和[**输出层**](https://developers.google.cn/machine-learning/crash-course/glossary#output_layer)（即预测）之间。神经网络包含一个或多个隐藏层。

![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/google-7.png)

#### 激活函数

这样添加隐藏层后，线性函数与线性函数的组合依然是线性的，所以我们通过添加激活函数（非线性转化层）来使模型可以处理非线性问题。

![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/google-8.png)

> 激活函数 (activation function)：一种函数（例如 [**ReLU**](https://developers.google.cn/machine-learning/crash-course/glossary#ReLU) 或 [**S 型**](https://developers.google.cn/machine-learning/crash-course/glossary#sigmoid_function)函数），用于对上一层的所有输入求加权和，然后生成一个输出值（通常为非线性值），并将其传递给下一层。
>
> ![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/google-9.png)
>
> ReLU函数：修正线性单元(Rectified Linear Unit)，规则为：F(x)=max(0,x)

激活函数的引入，在非线性上堆叠非线性，使得模型可以处理更为复杂的输出预测

实际上所有的函数都可以作为激活函数，我们假设激活函数 $\sigma$ ，网络中节点的值为 $v$ :

![](https://github.com/Dinghow/MyRoadToMachineLearning/raw/master/note/img/17.png)

#### 组件

神经网络包括：

- 一组节点$v$，类似于神经元，位于层中。
- 一组权重$w$，表示每个神经网络层与其下方的层之间的关系。下方的层可能是另一个神经网络层，也可能是其他类型的层。
- 一组偏差$b$，每个节点一个偏差。
- 一个激活函数$\sigma$ ，对层中每个节点的输出进行转换。不同的层可能拥有不同的激活函数。