# Transformer from Scratch

I implemented scaled dot-product attention, multi-head attention, feed-forward networks, sinusoidal positional encoding, and six-layer encoder and decoder stacks.

- [Notebook](transformer.ipynb)
- [Original Colab](https://colab.research.google.com/drive/1jEmb9UCrsre20SnR6k2kZKjU_YpJvpql)
- Source file: Transformer_From_Scratch.ipynb

## Implementation

The model uses a hidden dimension of 512, 8 attention heads, a feed-forward dimension of 2048, and dropout of 0.1. The final example uses a source sequence of length 4 and a target sequence of length 3, with intended output shapes of (4,512) and (3,512).

Install requirements.txt and run the notebook in order in Jupyter or Colab. These shapes describe the intended behavior; I have not yet validated the forward pass in this version.

## Known issues

- W_Q/W_K/W_V/W_O are all initialized to zero, making the attention branch degenerate. They need appropriate nonzero initialization.
- MultiHeadAttention.forward accepts mask but does not pass it to Attention, so the decoder's causal mask is not applied.
- Attention uses K.T and two-dimensional loops, supporting only unbatched two-dimensional inputs. A general implementation should operate on the final two dimensions.
- PE creates its tensor on the CPU. It needs to match the input's device and dtype for GPU execution.
- The decoder currently returns hidden states. A vocabulary projection, training loss, data pipeline, and evaluation are still missing.

This is a component implementation. My next checks will cover output shapes, gradients, and whether changing future tokens leaves earlier outputs unchanged. I have not reproduced the original paper's training results.

---

# Transformer from Scratch

我手写了缩放点积注意力、多头注意力、FFN、正弦位置编码及六层 Encoder/Decoder。

- [Notebook](transformer.ipynb)
- [原始 Colab](https://colab.research.google.com/drive/1jEmb9UCrsre20SnR6k2kZKjU_YpJvpql)
- 原文件：Transformer_From_Scratch.ipynb

## 当前实现

隐藏维度 512、8 个注意力头、FFN 维度 2048、dropout 0.1。末尾使用源序列长度 4、目标序列长度 3 的示例，设计输出为 (4,512) 和 (3,512)。

安装 requirements.txt 后在 Jupyter/Colab 中顺序运行。以上形状为代码设计预期，本次未执行前向传播。

## 已知问题

- 多头注意力的 W_Q/W_K/W_V/W_O 全部零初始化，注意力分支退化，需要合理的非零初始化。
- MultiHeadAttention.forward 接收 mask，但调用 Attention 时未传递，Decoder 的因果掩码实际不生效。
- Attention 使用 K.T 和二维循环，只适用于无 batch 的二维输入；通用实现应处理最后两个维度。
- PE 在 CPU 创建张量，迁移 GPU 时需要匹配输入的 device/dtype。
- 当前 Decoder 输出隐藏状态，尚无词表输出层、训练损失、数据管线与评测。

这是组件级实现，不是完整训练结果复现。下一步应检查前向形状、梯度，以及改变未来 token 后前面位置输出是否保持不变。
