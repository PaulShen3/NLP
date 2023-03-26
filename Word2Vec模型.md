## 上期回顾：神经网络语言模型NNML-->为了预测下一个词

得到了一个副产品(词向量)

Q矩阵，对于任何一个独热编码的词向量都可以通过Q矩阵得到新的词向量

1.可以转换维度

2.相似词之间的词向量有了关系

# Word2Vec模型--》为了得到词向量

神经网络语言模型-->主要目的就是为了得到词向量

![image-20230226195417395](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230226195417395.png)

NNLM和Word2Vec基本一模一样，不考虑细节，网络架构就是一模一样的

## CBOW

给出一句话的上下文，得到这个词

根据“我是最__的Paul”

预测出"帅" w_t

## skip-gram

给出一个词，得到这个词的上下文

根据"帅"

预测出"我是_的Paul"

## NNLM和Word2Vec区别

NNLM -->重点是预测下一个词，双层感知机

Word2Vec-->CBOW和skip-gram的重点是得到一个Q矩阵，SoftMax(w1(xQ)+b1)

1.CBOW：一个老师告诉多个学生，Q矩阵怎么变

2.Skip-gram:多个老师告诉一个学生，Q矩阵怎么变

# Word2Vec的缺点

Q矩阵的设计

![image-20230226202010657](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230226202010657.png)

00010代表apple x Q = 10,12,19  

apple（苹果，🍎）  就是吃的苹果和苹果手机，都说苹果，但是00010是吃的苹果，10，12，19就不知道了

(训练)假设数据集里只有苹果这个意思，但没有🍎这个意思

(测试，应用)apple,表示🍎这个意思

所以缺点就是词向量不能进行多意 --》ELMO模型