# 1、Transformer

Transformer是Seq2Seq类型的一种模型。

## 1.1、self-attention自注意力机制

<img src="/Users/zhangshuheng/Desktop/Notebooks/机器学习ML/李宏毅Tutorial/18Transformer.assets/image-20220119154136114.png" alt="image-20220119154136114" style="zoom:50%;" />

<img src="/Users/zhangshuheng/Desktop/Notebooks/机器学习ML/李宏毅Tutorial/18Transformer.assets/image-20220121172224191.png" alt="image-20220121172224191" style="zoom:50%;" />

## 1.2、Sequence2Sequence

输入是一个向量序列输出有三种情况：

1. 输出是一个label，如对文章进行标注是好评还是差评。
2. 输出的向量个数与输入向量个数一致。如给一段文字的每个单词做词性标注
3. 输出的向量个数不确定，由机器自己决定。就叫**Sequence2Sequence**，如翻译和对话机器人和语音识别。

## 1.3、Sequence2Sequence model

<img src="/Users/zhangshuheng/Desktop/Notebooks/机器学习ML/李宏毅Tutorial/18Transformer.assets/image-20220119161258889.png" alt="image-20220119161258889" style="zoom:50%;" />

包含一个Encoder和一个Decoder

<img src="/Users/zhangshuheng/Desktop/Notebooks/机器学习ML/李宏毅Tutorial/18Transformer.assets/image-20220119164637952.png" alt="image-20220119164637952" style="zoom:50%;" />

### 1.3.1、Encode

<img src="/Users/zhangshuheng/Desktop/Notebooks/机器学习ML/李宏毅Tutorial/18Transformer.assets/image-20220119162545173.png" alt="image-20220119162545173" style="zoom:50%;" />

### 1.3.2、Decode

decode都是把encode的最后一层作为decode的k，v。其实也可以用其他的方式来实现，也是一种研究方向。

<img src="/Users/zhangshuheng/Desktop/Notebooks/机器学习ML/李宏毅Tutorial/18Transformer.assets/image-20220119164549421.png" alt="image-20220119164549421" style="zoom:50%;" />

## 1.3、NLP（natural language procession）

