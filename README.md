# paper-implementations

论文方法实现与学习实验。按项目独立组织，当前收录从 Google Drive 导入的三个 Notebook。

| 项目 | 内容 | 当前状态 |
| --- | --- | --- |
| [Adversarial Training](adversarial-training/) | MNIST、Maxout、FGSM 与对抗训练 | 原始实现归档；已识别评估与训练流程问题，结果待重新验证 |
| [Transformer](transformer/) | 从零实现 Attention、Encoder、Decoder | 组件实现；掩码与初始化待修复，不代表原论文训练结果复现 |
| [GPT-2 Generation](gpt2-generation/) | 预训练 GPT-2 生成、困惑度与候选筛选 | 学习实验；自定义生成函数待修复，不属于模型提取攻击 |

## 使用方式

进入项目目录阅读 README，再打开对应 Notebook。各项目独立安装依赖，也可以使用 README 中的 Colab 原始入口。依赖列表仅从代码导入推导，未锁定已验证环境版本。

本次整理保留代码单元内容与顺序，清除了运行输出、执行计数和运行环境元数据；没有重新训练模型或验证历史指标。各项目的已知问题见其 README，不能将归档状态视为可完整复现。

## 范围

本仓库收录上述三个项目。原创数据集扰动实验、课程作业和其他研究材料不在本次整理范围内。

## 整理记录

2026-10-27：从 Drive 的 paper-implementations 文件夹导入三个 Notebook，完成 JSON 与 Python 单元语法检查，添加项目说明与待办清单。尚未执行端到端训练、模型下载或性能评测。
