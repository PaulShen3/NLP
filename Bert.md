# Bert

Bert的意义：从大量无标记数据集中训练得到的深度模型，可以显著提高各项自然语言处理任务的准确性。

## BERT集了哪些大成？

参考了ELMO模型的双向编码思想、借鉴了GPT用Transformer作为特征提取器的思路，采用了word2vec所使用的CBOW方法

## BERT和GPT和ELMo的区别

<img src="C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230227200358759.png" alt="image-20230227200358759" style="zoom:150%;" />

## 单项编码和双向编码

举例：

今天天气很{}，我们不能出去运动。

单项编码：只考虑上文

双向编码：考虑上下文

self-attention时可以看到上下文的

![image-20230303164323887](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230303164323887.png)

# BERT模型的详细结构图

![image-20230303164437909](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230303164437909.png)

bert和elmo都是为了获取特征向量，用transformer的编码进行特征提取，不断提取得到多重信息。

Bert最后得到是特征向量，所以可以在下游加任务

Bert的模型结构其实就是transformer Encoder模块的堆叠，在模型参数选择上，论文给出了两套不一致的模型。

参数已经定死了，拿来用就行

Bert的训练

bert是二段式训练：

第一阶段：使用以获取的大规模无标签语料，来训练基础语言模型

第二阶段：根据指定任务的少量带标签的训练数据集进行微调训练

## BERT为什么要做语言掩码模型(MLM)



双向编码器无法使用完形填空(CROW)的思想

对于一句话，我输入的时候mask掉15%的词(token),然后让模型预测这个token是什么（训练阶段的时候才会这样做，但是测试阶段没有mask的词）

## BERT的下句预测(NSP)

NSP的具体做法是：Bert输入的语句由两个句子构成，其中50%的概率讲寓意连贯的两个连续剧子作为训练文本，另外50%的概率将完全随机抽取两个句子作为训练文本

## BERT的下游任务改造

bert根据自然语言处理下游任务的输入和输出的形式，将微调训练支持的任务分为4类，分别是句对分类，单句分类，文本问答和而单句标注。

**句对分类**

给定两个句子，判断他们的关系，成为句对分类，判断句对是否相似，判断后者是否为前者的答案。

针对该问题，bert的预训练过程中使用NSP训练方法获得了直接捕获对语义关系的能力。

**单据分类**

给定一个句子，判断该句子的类别，例如判断情感类别。

针对单句二分类问题，也无需对bert的输入数据和输出数据的结构做任何改动

如下图所示，单据分类在句首u加入标签CLS，将句首标签所对应的输出值作为分类标签，计算预测分类标签与真是分类标签的交叉熵，将其作为优化目标，在任务数据上进行微调训练。

![image-20230303171751323](C:\Users\Jay Shen\AppData\Roaming\Typora\typora-user-images\image-20230303171751323.png)

同样，针对多分类问题，需要在句首标签cls的输出特征向量后接一个全连接层和softmax层，保证维数与类别数目一致，最后通过argmax操作得到相对应的类别结果。

bert借鉴了elmo，gpt，cbow，主要提出了masked语言模型和next sentence prediction。Bert没有什么大的创新，更像最近几年nlp重要进展的集大成者。

bert的两阶段模型：

第一阶段：双向语言模型预训练

第二阶段：采用具体任务fine-tuning或者做特征集成