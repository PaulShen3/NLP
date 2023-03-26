# Masked self-Attention

为什么要做这个改进：生成模型，生产单词，一个一个生成的

当我们做生成任务的时候，我们也相对生成的单词做注意力计算，但是生成的句子是一个一个单词生成的

I have  a dream

1.I   第一次注意力计算，只有I

2.I have  第二次，只有I和have

3.I have a   

4.I have a dream

5.I have a dream<eos>

掩码自注意力机制应运而生。

自注意力机制明确知道这句话有多少个单词，并且一次性给足，而掩码是分批次给，最后一次才给足。

