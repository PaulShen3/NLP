# Transformer框架概述

预训练--》NNLM-->word2Vec--》ELMo--》Attention

NLP种预训练的目的其实就是为了生成词向量

总分总

seq2seq

序列(编码器)到序列(解码器)

分成两部分，编码器和解码器



![image-20230227131346415](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227131346415.png)

# 机器翻译流程(Transformer)

通过机器翻译来作解释

给一个输入，给出一个输出，输出是输入的翻译的结果

“我是一个学生”-->(通过Transformer)I am a student



![image-20230227131807396](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227131807396.png)

编码器和解码器

编码器：把输入变成一个词向量（self-attention）

解码器：得到编码器输出的词向量后，生成翻译的结果

![image-20230227131649568](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227131649568.png)

Nx的意思是，编码器里面又有N个小编码器（默认N=6）

通过6个编码器，对词向量一步又一步的强化(增强)

流程3

![image-20230227132115820](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227132115820.png)

通过6个encoder获得一个增强的词向量给decoder

了解transformer就是了解transformer里的小的编码器和小的解码器

FFN（Feed Forward）: w2((w1x+b1))+b2

![image-20230227132223069](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227132223069.png)

