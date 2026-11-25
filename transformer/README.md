# Transformer from Scratch

[Notebook](transformer.ipynb) · [Current Colab](https://colab.research.google.com/drive/1y_ep9CyV6IdJu6n-Y5Matnh5IiVeHtgU)

Component implementation with d_model=512, 8 heads, FFN dimension 2048, six encoder/decoder layers and dropout=0.1.

## Corrections and checks

Q/K/V/O projections now receive Xavier uniform initialization. MultiHeadAttention forwards the mask argument, and Attention applies causal masking only for mask=True. Key transposition uses the final two dimensions.

Saved Colab outputs synced on 2026-11-13 show:
- Encoder/decoder shapes (4,512) and (3,512).
- Changing the final target token leaves the first two outputs unchanged (maximum difference 0.0 in this example).
- All attention projection matrices have finite, nonzero gradient absolute sums in the standalone attention check.

These are basic checks recorded in Colab, not independent reruns or comprehensive correctness tests.

## Running and scope

Install `torch` and run cells in order. Recreate model instances after changing class definitions.

The current example uses unbatched CPU inputs. Mask loops and positional encoding do not yet support general batched inputs; positional encoding creates a CPU tensor without matching input device/dtype. There is no padding mask, vocabulary output projection, training task or end-to-end learning evaluation. This is a component implementation, not a reproduction of the paper's training results.

---

# 手写 Transformer 组件

已修复注意力投影零初始化及 mask 传递，使用 Xavier 初始化和最后两维转置。

当前 Colab 保存了前向形状 (4,512)/(3,512)、未来 token 改动对前两个位置影响为 0.0，以及各注意力投影矩阵收到非零有限梯度的检查输出。本次同步保留这些输出，没有重新执行或训练。

当前范围是 CPU 上的单条序列组件验证；尚未支持完整 batch/padding mask，位置编码仍在 CPU 创建，尚无词表输出层与训练任务。安装 `torch` 后按顺序执行；修改类后须重新创建模型。不宣称完整复现原论文。
