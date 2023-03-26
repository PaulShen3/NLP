# Attention(注意力机制)

你会注意什么？

大数据（什么数据都有，重要的，不重要的）

对于重要的数据我们要使用

对于不重要的数据，我们不太想使用

但是，对于一个模型而言(CNN,LSTM)，很难决定什么重要，什么不重要

由此，注意力机制诞生了。(有人发现了如何去在深度学习的模型上做注意力)

![image-20230227095132894](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227095132894.png)

红色的是科学家们发现，如果给你一张这个图，你眼睛会聚焦在红色区域

人--》看脸

文章看标题，段落看开头，后面的落款

这些红色区域可能包含更多/更重要的信息

注意力机制：我们会把我们的焦点聚焦在比较重要的事物上

## 怎么做注意力

我(查询值Q)，这张图(被查询对象V)

我看这张图，第一眼我就会去判断那些东西对我而言更重要，哪些对我而言更不重要

(去计算Q和V里事物的重要度)

重要度计算，其实就是相似度计算，点乘其实就是求内积（不要关心为什么可以）

Q，K我们一般使用点乘的方式
$$
K = k_1,k_2,\cdots,k_n
$$
通过点乘的方法计算Q和K里的每一个事物的相似度，就可以拿到Q和k1的相似值$a_1$，Q和k2的相似值$a_2$，Q和$k_n$的相似值$a_n$

做一层 
$$
softmax(a_1,a_2,\cdots,a_n)
$$
就可以得到概率，进而得到哪个对Q更重要

![image-20230227095839631](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227095839631.png)

我们还得进行一个汇总，当你使用Q查询结束了后，Q已经失去了它的使用价值，我们最终还是要拿到这张图片，只不过现在的这张图片多了一些信息

(多了于我而言更重要，更不重要的信息在这里)

$ \ softmax(a_1,a_2,\cdots,a_n) $

$(a_1,a_2,\cdots,a_n)*+(v_1,v_2,\cdots,v_n)=(a_1*v_1+a_2*v_2+\cdots+a_n*v_n)=V'$

这样的话就得到了一个新的V，这个新的V就包含了哪些更重要，哪些不重要的信息在里面,然后用V‘代替V

一般K=V，在transformer里，K！=V也可以，但是K和V之间要有联系

 ![image-20230227102743617](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227102743617.png)

QK相乘求相似度，做一个scale(未来做softmax的时候避免出现极端情况)

然后做softmax得到概率

新的向量表示了K和V(K==V)，然后这种表示还暗含了Q的信息(于Q而言，K里面重要的信息)，也就是说，挑出了K里面的关键点

# 自-注意力机制(self-Attention)(向量)

self-attention的关键点在于，不仅仅是K$\approx$V$\approx$Q来源于同一个X,这三者是同源的，

通过X找到X里面的关键点

并不是K=V=Q=X,而是通过三个参数$W_Q,W_K,W_V$

![image-20230227103210198](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227103210198.png)

![image-20230227103329609](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227103329609.png)

![image-20230227103348759](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227103348759.png)

![image-20230227103421085](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227103421085.png)

$z_1$表示的就是thinking的新的向量表示

对于thinking，初始词向量为$x_1$

现在我通过thinking machines这句话去查询这句话里每一个单词和thinking之间的相似度

新的$z_1$依然是thinking的词向量的表示，只不过这个词向量的表示蕴含了thinking machines这句话对于thinking而言哪个更重要的信息 

<img src="C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227104234788.png" alt="image-20230227104234788" style="zoom:50%;" />

<img src="C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227104254758.png" alt="image-20230227104254758" style="zoom:50%;" />

# 注意力机制和自注意力机制的区别

注意力机制是一个很宽泛的概念，QKV相乘就是注意力，但是没有规定QKV是怎么来的

通过一个查询变量Q，去找到V里面比较重要的东西

先假设K==V，然后QK相乘得到相似度A，然后AV相乘得到注意力值Z，这个Z就是V的另一种表示

Q可以是任何一个东西，V也是任何一个东西，K往往是等同于V的(同源)，K和V不同源不相等可不可以

## 自注意力机制

自注意力机制特别狭隘

本质上QKV可以看作是相等的

对于一个词向量(不一定准确),做的是空间上的对应，乘上了参数矩阵，依然代表X

不仅规定了QKV同源，而且规定了QKV的做法

# 交叉注意力机制

Q和V不同源，但是K和V同源

# cyd注意力机制

Q和V同源，Q和K不同源

# xxx注意力机制

Q必须为1，K和V不同源

# RNN和LSTM与注意力机制的区别

![image-20230227123758246](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227123758246.png)

无法做长序列，当一段话达到50个字，效果就很差了

![image-20230227123849484](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227123849484.png)

LSTM通过各种门选择性的可以记忆之前的信息(200词)

# Attention和RNNs(RNN,LSTM)的区别

RNNS长序列以来问题，无法做并行

self-attention得到新的词向量具有句法特征和语义特征(表征更完善)

## 句法特征

![image-20230227124049945](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227124049945.png)

## 语义特征

![image-20230227124147358](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227124147358.png)

## 并行计算

