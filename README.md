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

我在这个仓库中整理自己学习深度学习时编写的模型实现和实验，包括基于 MNIST 的 FGSM 对抗训练复现和从零实现的 Transformer 组件。

### 项目

| 项目 | 我实现的内容 | 当前进度 |
| --- | --- | --- |
| [对抗训练](adversarial-training/) | Maxout 网络、FGSM 攻击、对抗样本训练与准确率评估
| [Transformer](transformer/) | 注意力、多头注意力、前馈网络、位置编码及 Encoder/Decoder

