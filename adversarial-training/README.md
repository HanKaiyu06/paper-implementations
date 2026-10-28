# Adversarial Training / FGSM

I implemented a Maxout network, FGSM attacks, and training on adversarial examples using MNIST.

- [Notebook](experiment.ipynb)
- [Original Colab](https://colab.research.google.com/drive/1zAywVl_M9CWkHQEgP-qjt8ZP9wjPOOZu)
- Source file: Adversarial_Training_FGSM.ipynb

## Experiment setup

The Maxout network has dimensions 784 → 240 → 240 → 10 with a pool size of 5. I use Adam with a learning rate of 0.001, a batch size of 128, and 5 epochs. FGSM uses epsilon = 0.07. MNIST is downloaded through torchvision and converted with ToTensor to pixel values in [0,1].

## Running the notebook

Install the dependencies in this directory's requirements.txt, then open experiment.ipynb in Jupyter or Colab. Running it downloads MNIST, trains the models, and saves maxout_mnist.pth. The issues below need to be addressed before I can report reliable reproduction results.

## Code review notes

Cell numbers start at 0.

- Cells 8 and 10: adversarial inputs are not clipped to [0,1]. Training and evaluation need the same perturbation constraints.
- Cells 11 and 12: a fixed adversarial training set is generated using the earlier model, then used to train a newly initialized model. For online adversarial training, attacks should instead be generated against the current model in each batch.
- Cell 15: total/correct are not reset, so the final accuracy includes counts from an earlier evaluation and is unreliable.
- Cell 5: evaluation should explicitly call model.eval(). The current network has no dropout or batch normalization, but the evaluation procedure should still be consistent.
- Both models need clean accuracy and white-box FGSM accuracy measured on the same test set at the same epsilon. Cell 14 already generates attacks against the new model; I will preserve this approach.
- Random seeds and environment versions have not been fixed or recorded. Results need to be rerun with documented settings.

## Next steps

I will first fix clipping and evaluation counters, specify whether the experiment uses online adversarial training or a fixed attack dataset, and reevaluate under consistent conditions. Only source-code syntax has been checked so far; I have not validated reproduction of the paper's results.

---

# Adversarial Training / FGSM

我基于 MNIST 实现了 Maxout 网络、FGSM 攻击和对抗样本训练。

- [Notebook](experiment.ipynb)
- [原始 Colab](https://colab.research.google.com/drive/1zAywVl_M9CWkHQEgP-qjt8ZP9wjPOOZu)
- 原文件：Adversarial_Training_FGSM.ipynb

## 实验设置

Maxout 784 → 240 → 240 → 10，pool size 5；Adam 学习率 0.001，batch size 128，训练 5 轮；FGSM epsilon = 0.07。MNIST 使用 ToTensor，像素范围为 [0,1]，由 torchvision 自动下载。

## 运行

安装本目录 requirements.txt，在 Jupyter 或 Colab 打开 experiment.ipynb。运行会下载 MNIST、训练模型并写入 maxout_mnist.pth。当前代码有下列已知问题，尚不提供可信的完整复现指标。

## 逐单元审查（从 0 编号）

- 单元 8、10：攻击后未裁剪至 [0,1]，需统一训练和测试的扰动约束。
- 单元 11、12：先用旧模型生成固定对抗训练集，再初始化新模型训练。这属于固定攻击数据训练；若目标是在线对抗训练，应在每个 batch 用当前模型生成攻击。
- 单元 15：未重置 total/correct，累计了先前评估的计数，最终准确率不可信。
- 单元 5：应显式调用 model.eval()；当前网络无 dropout/BN，但评估流程需要规范。
- 比较时应为两个模型分别报告干净准确率及相同 epsilon、同一测试集上的白盒 FGSM 准确率。单元 14 已针对新模型生成攻击，需保留这一原则。
- 未固定随机种子、未保存环境版本；需要重跑并记录设置，不能直接沿用历史输出。

## 下一步

先修复裁剪与计数，明确在线对抗训练还是固定攻击数据训练，再在相同条件下重新评估。当前只确认源代码语法，不声称复现原论文结果。
