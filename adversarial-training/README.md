# FGSM Adversarial Training on MNIST

[Notebook](experiment.ipynb) · [Colab](https://colab.research.google.com/drive/1t3xJMWpFZiRjybRakVu-a2RMjRSYjtAL)

I implemented a Maxout network and FGSM adversarial training, then added PGD-20 to compare single-step and multi-step attacks.

## Setup

- Model: 784 → 240 → 240 → 10, Maxout pool size 5.
- Dropout: 0.2 on the input, 0.5 after each Maxout layer.
- Training: Adam, learning rate 0.001, batch size 128, 5 epochs per model, seed 42.
- Adversarial training: FGSM samples generated for each batch against the current model; loss = 0.5 × clean loss + 0.5 × adversarial loss.
- Training and evaluation perturbation budget: L∞ ε = 0.25. Pixels are clipped to [0, 1].
- PGD: 20 steps, step size ε/4 = 0.0625, one random start, projection to the ε-neighborhood of the original image.
- Dropout is active during training, including FGSM generation, and disabled during test attack generation and evaluation.

## Results

Saved notebook outputs from one training run per model, evaluated on all 10,000 MNIST test images. White-box attacks are generated separately against each evaluated model.

| Model | Clean accuracy | FGSM accuracy | PGD-20 accuracy |
| --- | ---: | ---: | ---: |
| Standard training | 97.87% | 4.06% | 0.01% |
| FGSM adversarial training | 97.33% | 72.81% | 2.12% |

FGSM adversarial training substantially improved FGSM accuracy, but PGD-20 still caused most inputs to be misclassified. The gap shows that FGSM evaluation alone does not adequately describe this model's robustness to multi-step attacks.

## Run

Install the dependencies in [requirements.txt](requirements.txt), then run the notebook from top to bottom. MNIST downloads automatically.

The notebook saves `maxout_mnist.pth` for the standard model and `maxout_mnist_fgsm_adv_eps025.pth` for the adversarially trained model in the runtime's working directory. These weights are generated when the notebook runs; they are not embedded in the notebook.

Reference: [Explaining and Harnessing Adversarial Examples](https://arxiv.org/abs/1412.6572).

---

# MNIST 上的 FGSM 对抗训练

我实现了 Maxout 网络和 FGSM 对抗训练，并加入 PGD-20，比较单步攻击和多步攻击下的分类表现。

## 实验设置

- 模型：784 → 240 → 240 → 10，Maxout pool size 为 5。
- Dropout：输入层丢弃概率为 0.2，两个 Maxout 层输出的丢弃概率均为 0.5。
- 训练：Adam，学习率 0.001，batch size 128，每个模型训练 5 轮，种子为 42。
- 对抗训练：每批针对当前模型生成 FGSM 样本，使用 0.5 × 干净损失 + 0.5 × 对抗损失。
- 训练与测试的扰动预算均为 L∞ ε=0.25，像素裁剪到 [0,1]。
- PGD：20 步，步长 ε/4=0.0625，一个随机起点，每步将扰动限制回原图的 ε 邻域。
- 训练及训练攻击生成时开启 Dropout；测试攻击生成和评估时关闭。

## 实验结果

以下来自 notebook 中保存的单次训练结果，在全部 10,000 张 MNIST 测试图片上评估。两种白盒攻击都分别针对被评估的模型生成。

| 模型 | 干净准确率 | FGSM 准确率 | PGD-20 准确率 |
| --- | ---: | ---: | ---: |
| 普通训练 | 97.87% | 4.06% | 0.01% |
| FGSM 对抗训练 | 97.33% | 72.81% | 2.12% |

FGSM 对抗训练明显提高了 FGSM 评估准确率，但 PGD-20 仍能让大部分样本被误分类。因此，单看 FGSM 表现不足以判断这个模型面对多步攻击时的鲁棒性。

## 运行

安装 [requirements.txt](requirements.txt) 中的依赖，按顺序运行 notebook，MNIST 会自动下载。

运行时会在当前目录生成普通模型权重 `maxout_mnist.pth` 和对抗模型权重 `maxout_mnist_fgsm_adv_eps025.pth`；权重文件不包含在 notebook 内。

参考论文：[Explaining and Harnessing Adversarial Examples](https://arxiv.org/abs/1412.6572)。
