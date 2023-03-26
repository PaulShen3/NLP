## 回顾：Word2Vec模型

NNLM模型(是不是在预测下一个词，副产品是词向量)

word2Vec模型：专门做词向量

1.CBOW

2.Skip-gram

但apple，苹果，🍎无法确定，是word2vec的缺陷，因此有了ELMo模型

# ELMo模型-->解决了多义词的问题



![image-20230226203348682](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230226203348682.png)

EMLo解决多义词问题

![image-20230226203416583](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230226203416583.png)

EMLo(专门做词向量，通过预训练)

不只是训练一个Q矩阵，我还可以把这个词的上下文信息融入到这个Q矩阵中

左边的LSTM获取E2的上文信息，右边就是下文信息

x1,x2,x4,x5-->word2Vec x1+x2+x4+x5 -->预测下一个词

获取上下文信息后，把三层的信息进行一个叠加

E1+E2+E3 = K1 一个新的词向量 ≈ E1

E2，E3相当于两个上下文信息

K1包含了第一个词的词向量包含单词特征、句法特征、语义特征

### 怎么用

E2，E3不同，E1+E2+E3不同

apple --> 我吃了一个 苹果 --> [1,20,10]   一般词向量是512维

apple --> 我在用苹果手机 --> [1,10,20]

![image-20230226204800208](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230226204800208.png)

LSTM 无法并行，长期依赖

Attention 解决了LSTM的问题