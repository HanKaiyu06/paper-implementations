# Deep Learning Implementations & Experiments

I use this repository to organize model implementations and experiments from my study of deep learning. It currently includes FGSM adversarial training on MNIST and Transformer components implemented from scratch.

Through implementation, code review, and experimental comparisons, I aim to develop a more concrete understanding of model architectures, training methods, and evaluation. Each project has its own notebook, dependency list, and notes on remaining work.

### Projects

| Project | What I implemented | Current status |
| --- | --- | --- |
| [Adversarial training](adversarial-training/) | A Maxout network, FGSM attacks, training on adversarial examples, and accuracy evaluation | Online FGSM and mixed clean/adversarial loss implemented; saved Colab results available; clipping and broader evaluation remain |
| [Transformer](transformer/) | Attention, multi-head attention, feed-forward networks, positional encoding, and encoder/decoder components | Initialization and mask propagation corrected; saved forward, causal and gradient checks available |

### Getting started

Read the README in each project directory before opening its notebook. Each project includes a separate requirements.txt and a link to the original Colab notebook. Dependencies were identified from imports; a verified environment has not yet been pinned.

### Status and next steps

On 2026-11-13, the adversarial-training and Transformer notebooks were synced from their current Colab versions with saved outputs preserved. Their READMEs distinguish recorded results from remaining limitations. This sync did not rerun training.

These projects document my implementation and learning process. The Transformer project currently covers components. I have not verified reproduction of the corresponding papers' experimental results.

---

# 深度学习实现与实验

我在这个仓库中整理自己学习深度学习时编写的模型实现和实验，包括基于 MNIST 的 FGSM 对抗训练和从零实现的 Transformer 组件。

我希望通过亲手实现、检查代码和对比实验结果，更具体地理解模型结构、训练方法与评估方式。每个项目单独保留 Notebook、依赖说明和待改进事项。

### 项目

| 项目 | 我实现的内容 | 当前进度 |
| --- | --- | --- |
| [对抗训练](adversarial-training/) | Maxout 网络、FGSM 攻击、对抗样本训练与准确率评估 | 已修复计数并采用在线 FGSM 与混合损失，保留 Colab 结果；裁剪与更全面评估待补充 |
| [Transformer](transformer/) | 注意力、多头注意力、前馈网络、位置编码及 Encoder/Decoder | 已修复初始化与掩码传递，保留前向、因果性与梯度检查输出 |

### 如何查看与运行

进入项目目录阅读 README，再打开 Notebook。每个项目都有独立的 requirements.txt 和原始 Colab 链接。依赖清单来自代码中的导入，尚未固定经过验证的环境版本。

### 进度与计划

2026-11-13：对抗训练和 Transformer 已同步当前 Colab 代码与保存输出，具体结果和剩余限制见各项目说明。本次同步未重新训练。

这些项目记录了我的实现与学习过程。Transformer 目前是组件级实现；我尚未验证它们达到对应论文的实验结果。
