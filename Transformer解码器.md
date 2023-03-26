# Transformer解码器decoder

![image-20230227135522102](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227135522102.png)

解码器的self-attention在编码已经生成的单词

加入目标词"我是一个学生"--》masked self-attention

训练阶段：目标词“我是一个学生”是已知的，然后self-attention是对“我是一个学生”做计算

测试阶段：

如果不做masked，每次训练阶段都会获得全部的信息

如果做masked，self-attention第一次对“我”做计算

self-attention第二次对“我是”做计算

![image-20230227140627989](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227140627989.png)

![image-20230227140636209](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227140636209.png)

![image-20230227140650146](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227140650146.png)