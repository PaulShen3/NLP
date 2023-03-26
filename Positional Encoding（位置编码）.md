# Positional Encoding（位置编码）

## Attention

1.解决了长序列依赖问题

2.可以并行

## 为什么需要位置编码

缺点：

1.开销变大了

2.既然可以并行，也就是说，词与词之间不存在顺序关系(打乱一句话，这句话里每一个词的词向量依然不会变)，即无位置关系(既然没有，我就用位置编码的形式去加一个)

出现的问题：位置编码的问题,对于每一个词而言都是无位置关系，把每个词的顺序打乱，得到的注意力值依然不变。

## 位置编码怎么做的

<img src="C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227125703056.png" alt="image-20230227125703056" style="zoom:150%;" />

# 具体做法

做法1：

$PE_(pos,2i)=sin(\frac{pos}{10000^\frac{2i}{d_(model)}})$

pos：位置，i：维度  $d_(model)$该模型词向量维度

$PE_(pos,2i+1)=cos(\frac{pos}{10000^\frac{2i}{d_(model)}})$

![image-20230227130018242](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227130018242.png)

![image-20230227130249173](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227130249173.png)