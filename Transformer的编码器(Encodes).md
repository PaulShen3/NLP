# Transformer的编码器(Encodes)

![image-20230227132715698](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227132715698.png)

编码器包括两个子层，self-attention、feed forward

每一个子层的传输过程中都会有一个残差网络+归一化

![image-20230227132824838](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227132824838.png)

Thinking--》得到绿色的X1（词向量，可以通过one-hot、word2vec得到）

--》叠加位置编码（给x1赋予位置属性）得到黄色的X1

--》输入到self-attention子层中，做注意力机制(x1,x2拼接起来的一句话)，得到z1(x1与x2拼接起来的句子做了自注意力机制的词向量，表征的仍然是thinking)，也就是说z1拥有了位置属性、句法特征、语义特征的词向量，得到粉色的z1

--》残差网络(避免梯度消失，w3(w2(w1x+b))+b2)+b3,如果w1，w2，w3特别小,x就没了，【w3(w2(w1x+b))+b2)+b3+x】),归一化 (LayerNorm)，做标准化（避免梯度爆炸），限制区间，得到了深粉色的z1

--》Feed Forward，Relu(w2(w1x+b))+b2)(前面每一步都在做线性变化wx+b)，线性变换的叠加永远都是线性变化，通过Feed Forward中的Relu做一次非线性变换,这样的空间变换可以无限拟合任意一种状态了，得到***$r_1$***

## 总结

transformer的encoders就是做词向量，只不过这个词向量更加优秀