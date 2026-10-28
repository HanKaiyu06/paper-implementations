# Adversarial Training / FGSM

基于 MNIST 的 Maxout 网络、FGSM 攻击与对抗训练学习实现。

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
