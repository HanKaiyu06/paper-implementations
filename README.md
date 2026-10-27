# Deep Learning Implementations & Experiments
# 深度学习实现与实验

## 中文

我在这个仓库中整理自己学习深度学习时编写的模型实现和实验，包括基于 MNIST 的 FGSM 对抗训练、从零实现的 Transformer 组件，以及 GPT-2 文本生成与困惑度实验。

我希望通过亲手实现、检查代码和对比实验结果，更具体地理解模型结构、训练方法与评估方式。每个项目单独保留 Notebook、依赖说明和待改进事项。

### 项目

| 项目 | 我实现的内容 | 当前进度 |
| --- | --- | --- |
| [对抗训练](adversarial-training/) | Maxout 网络、FGSM 攻击、对抗样本训练与准确率评估 | 初版代码已整理；需要修正扰动裁剪、评估计数，并明确训练方案后重新评测 |
| [Transformer](transformer/) | 注意力、多头注意力、前馈网络、位置编码及 Encoder/Decoder | 组件实现已整理；需要修正掩码传递和参数初始化，补充前向与梯度检查 |
| [GPT-2 生成](gpt2-generation/) | 预训练模型采样、困惑度计算、候选排序及温度递减生成函数 | 实验代码已整理；自定义生成函数的维度处理与边界条件需要修正 |

### 如何查看与运行

进入项目目录阅读 README，再打开 Notebook。每个项目都有独立的 requirements.txt 和原始 Colab 链接。依赖清单来自代码中的导入，尚未固定经过验证的环境版本。

### 进度与计划

我保留了初版代码，并清除了旧运行输出，便于后续逐项修正和重新记录结果。目前只完成了 Notebook 格式和 Python 单元语法检查，尚未完成端到端运行验证。我会先修正对抗训练的评估流程，再检查 Transformer 和 GPT-2 实验。

这些项目记录了我的实现与学习过程。Transformer 目前是组件级实现，GPT-2 项目使用预训练模型；我尚未验证它们达到对应论文的实验结果。

## English

I use this repository to organize model implementations and experiments from my study of deep learning. It currently includes FGSM adversarial training on MNIST, Transformer components implemented from scratch, and experiments with GPT-2 text generation and perplexity.

Through implementation, code review, and experimental comparisons, I aim to develop a more concrete understanding of model architectures, training methods, and evaluation. Each project has its own notebook, dependency list, and notes on remaining work.

### Projects

| Project | What I implemented | Current status |
| --- | --- | --- |
| [Adversarial training](adversarial-training/) | A Maxout network, FGSM attacks, training on adversarial examples, and accuracy evaluation | Initial code organized; perturbation clipping and evaluation counters need correction, followed by a clearly specified training setup and new evaluation |
| [Transformer](transformer/) | Attention, multi-head attention, feed-forward networks, positional encoding, and encoder/decoder components | Components organized; mask propagation and parameter initialization need correction, followed by forward-pass and gradient checks |
| [GPT-2 generation](gpt2-generation/) | Sampling from a pretrained model, perplexity calculation, candidate ranking, and a temperature-decay generation function | Code organized; the custom generation function needs tensor-shape fixes and input validation |

### Getting started

Read the README in each project directory before opening its notebook. Each project includes a separate requirements.txt and a link to the original Colab notebook. Dependencies were identified from imports; a verified environment has not yet been pinned.

### Status and next steps

I have retained the initial code and cleared its saved outputs so that I can document corrections and new results explicitly. Notebook structure and Python cell syntax have been checked, but end-to-end execution has not yet been validated. My next priority is the adversarial-training evaluation pipeline, followed by the Transformer and GPT-2 experiments.

These projects document my implementation and learning process. The Transformer project currently covers components, and the GPT-2 project uses a pretrained model. I have not verified reproduction of the corresponding papers' experimental results.
