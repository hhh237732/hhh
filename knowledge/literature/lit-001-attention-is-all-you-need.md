---
id: lit-001
title: 《Attention Is All You Need》阅读笔记
type: literature
created: 2026-04-06
tags: [NLP, Transformer, 深度学习, 自注意力]
source: "https://arxiv.org/abs/1706.03762"
author: "Vaswani et al. (Google Brain, 2017)"
status: stable
---

# 《Attention Is All You Need》阅读笔记

## 基本信息

| 字段 | 内容 |
|------|------|
| 标题 | Attention Is All You Need |
| 作者 | Ashish Vaswani et al. |
| 机构 | Google Brain / Google Research |
| 发表 | NeurIPS 2017 |
| 链接 | https://arxiv.org/abs/1706.03762 |

## 核心贡献

1. 提出了完全基于**自注意力机制（Self-Attention）**的序列转换模型 **Transformer**，摒弃 RNN 和 CNN。
2. 引入**多头注意力（Multi-Head Attention）**，让模型从不同表示子空间学习依赖关系。
3. 在机器翻译任务上大幅超越当时 SOTA，且训练速度更快（支持高度并行）。

## 方法/内容摘要

### 整体架构

Transformer 采用 **Encoder-Decoder** 结构：

- **Encoder**：N 层堆叠，每层含多头自注意力 + 前馈网络（FFN），均带残差连接与层归一化。
- **Decoder**：N 层堆叠，额外包含**掩码多头自注意力**（防止看到未来信息）和**交叉注意力**（对接 Encoder 输出）。

### 缩放点积注意力（Scaled Dot-Product Attention）

$$\text{Attention}(Q, K, V) = \text{softmax}\!\left(\frac{QK^\top}{\sqrt{d_k}}\right)V$$

除以 $\sqrt{d_k}$ 是为了防止 $d_k$ 较大时点积值过大导致梯度消失。

### 多头注意力

将 Q、K、V 投影到 $h$ 个子空间，分别计算注意力后拼接再投影：

$$\text{MultiHead}(Q,K,V) = \text{Concat}(\text{head}_1,\ldots,\text{head}_h)W^O$$

### 位置编码（Positional Encoding）

由于无序列归纳偏置，需手动注入位置信息。论文使用正弦/余弦函数：

$$PE_{(pos,2i)} = \sin(pos/10000^{2i/d_{model}})$$

## 关键结论

- WMT 2014 英→德翻译达到 **28.4 BLEU**，超越所有已有模型。
- 训练成本（FLOP）比同期最优 RNN 模型低一个数量级。
- 该架构后来成为 BERT、GPT 系列的基础。

## 个人笔记

- 自注意力的全局感受野是相对于 RNN 最大的优势，但序列长度的 $O(n^2)$ 内存开销在长文本场景仍是瓶颈。
- 位置编码的设计让模型可以推广到训练时未见过的序列长度（相对位置信息）。
- 后续工作（RoPE、ALiBi 等）对位置编码做了大量改进。

## 参考资料

- [arXiv 原文](https://arxiv.org/abs/1706.03762)
- [The Illustrated Transformer (Jay Alammar)](https://jalammar.github.io/illustrated-transformer/)
