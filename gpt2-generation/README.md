# GPT-2 Generation and Perplexity

I use pretrained GPT-2 to explore text sampling, perplexity, and candidate ranking. This project covers generation experiments, not model extraction attacks.

- [Notebook](experiment.ipynb)
- [Original Colab](https://colab.research.google.com/drive/1F9Gjw44VWP9w1EKH77zZr8nPS6xk2XRo)
- Source file: GPT2_Generation_and_Perplexity.ipynb

## Running the experiment

Install requirements.txt and open the notebook in Jupyter or Colab. The first run needs internet access to download the gpt2 model and tokenizer. The notebook's installation cell installs transformers and accelerate; the dependency file also includes torch, which the code imports.

The default experiment samples 100 candidates from the prompt The, with up to 30 new tokens per candidate and top-k=40, then ranks them by the model's own perplexity. I also defined a temperature-decay generation function, but the candidate-generation cell calls model.generate rather than this custom function.

## Known issues and interpretation

- The custom generation function concatenates two-dimensional input_ids with one-dimensional next_token, causing a shape mismatch. Decoding should also receive a single sequence.
- decay_steps=1 causes division by zero. Temperature, top_k, and length parameters need validation.
- Perplexity calculation needs to handle texts with fewer than 2 tokens and inputs beyond the context window. A numerically stable cross-entropy calculation in inference mode would be preferable.
- Generation and scoring should explicitly use model.eval() with gradients disabled. Random seeds and environment versions also need to be recorded.
- Ranking a model's own samples by its perplexity does not establish improvements in factual accuracy, quality, or safety.

The current version has been organized and statically reviewed. I have not rerun model loading or generation, and no new experimental results are reported.

---

# GPT-2 Generation and Perplexity

我使用预训练 GPT-2，进行文本采样、困惑度计算和候选排序。这是生成实验，不是 Model Extraction Attack。

- [Notebook](experiment.ipynb)
- [原始 Colab](https://colab.research.google.com/drive/1F9Gjw44VWP9w1EKH77zZr8nPS6xk2XRo)
- 原文件：GPT2_Generation_and_Perplexity.ipynb

## 运行与内容

安装 requirements.txt，在 Jupyter/Colab 中运行。首次使用需要联网下载 gpt2 模型及 tokenizer。原 Notebook 的安装单元安装 transformers 与 accelerate；本目录同时列出代码使用的 torch。

默认从提示词 The 采样 100 个候选，每个最多新增 30 tokens，top-k=40，然后按模型自身困惑度排序。原文件还定义了温度递减生成函数，但候选生成单元实际调用 model.generate，没有使用该函数。

## 已知问题与解释边界

- 自定义生成函数将二维 input_ids 与一维 next_token 拼接，会发生维度不匹配；解码也应传入单条序列。
- decay_steps=1 会发生除零；温度、top_k 和长度需要参数校验。
- 困惑度计算需处理少于 2 tokens、超出上下文窗口的文本；建议使用稳定的交叉熵计算并在推理模式下执行。
- 生成和打分应显式设 model.eval() 并关闭梯度，固定随机种子及环境版本。
- 同一模型生成后再按自身困惑度筛选，不能据此证明文本事实性、质量或安全性提升。

本次仅完成归类与静态审查，未重新下载模型或运行生成，未报告新的实验结果。
