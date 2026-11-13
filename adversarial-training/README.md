# Adversarial Training / FGSM

[Notebook](experiment.ipynb) · [Current Colab](https://colab.research.google.com/drive/1t3xJMWpFZiRjybRakVu-a2RMjRSYjtAL)

I implemented Maxout and FGSM on MNIST, then corrected evaluation counters and replaced fixed attack-dataset training with online attacks against the current model. The training objective is 0.5 × clean loss + 0.5 × adversarial loss.

## Setup and saved results

Maxout: 784 → 240 → 240 → 10, pool size 5; Adam lr=0.001; batch size 128; 5 epochs per model; epsilon=0.07. Inputs use ToTensor. Attacks are **not clipped** to [0,1].

| Model | Clean accuracy | White-box FGSM accuracy |
| --- | ---: | ---: |
| Standard training | 97.52% | 18.96% |
| Online FGSM + mixed loss | 98.86% | 91.23% |

These are outputs saved in the current Colab snapshot, synced on 2026-11-13, not an independently rerun benchmark or multi-seed average. Test attacks are regenerated against each evaluated model. The final adversarial evaluation records 9,123 correct out of 10,000.

Install requirements.txt and run the notebook from top to bottom; MNIST downloads automatically. The checkpoint maxout_mnist.pth is saved for the standard model before the model variable is replaced.

## Limitations

Seeds and verified dependency versions are not pinned. No PGD evaluation or repeated-run statistics are included. The network has no dropout or batch normalization; some evaluation/attack-generation cells do not explicitly set eval mode. Pixel clipping remains unimplemented. Results do not establish robustness to stronger attacks or reproduce the original paper's experimental setup.

Reference: [Explaining and Harnessing Adversarial Examples](https://arxiv.org/abs/1412.6572).

---

# FGSM 对抗训练

已修复评估计数，改为每批针对当前模型生成攻击，并使用各占一半的干净与攻击损失。固定攻击训练集生成代码已从当前 Colab 删除。

当前保存输出：普通模型干净/攻击准确率为 97.52% / 18.96%；在线对抗训练模型为 98.86% / 91.23%。以上来自本次同步的 Colab 输出，未在同步时重新训练，不是多种子统计。

设置为 Maxout 两层 240 单元、pool size 5、Adam 学习率 0.001、batch size 128、各训练 5 轮、epsilon=0.07。攻击未裁剪至 [0,1]。运行会下载 MNIST；保存的权重属于普通模型。

尚未固定种子与环境版本、开展 PGD 评估或多次重复实验；不宣称完整复现论文。按顺序运行 Notebook，避免沿用旧模型的攻击测试集。
