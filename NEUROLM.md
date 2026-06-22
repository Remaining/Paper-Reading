---
title: "NEUROLM: A UNIVERSAL MULTI-TASK FOUNDATION MODEL FOR BRIDGING THE GAP BETWEEN LANGUAGE AND EEG SIGNALS"
link: "[https://arxiv.org/pdf/2409.00101]"
date: 2026-06-22
author: qiuyun zhang
tags: ["EEG", "Foundation model"]
---

## 一句话总结内容

针对现有 EEG 基座模型通常依赖任务特定微调、难以在多类脑电任务之间统一建模与迁移的问题，提出了基于离散神经信号的通用脑电-语言基础模型 NeuroLM。该方法首先将连续 EEG 信号转换为可被语言模型处理的离散 neural tokens，结合多任务指令微调，将异常检测、事件分类、情绪识别、睡眠分期、认知负荷识别等任务统一为“EEG token + 文本指令 + 答案”的生成式预测范式。通过在 TUAB、TUEV、SEED、HMC、Workload 和 TUSL 等多个 EEG 下游任务上的系统评估，验证了 NeuroLM 能够在一个统一模型中完成多类 EEG 任务，并在部分任务上取得接近专用模型的性能，表明将 EEG 信号与大语言模型进行统一建模具有可行性和潜在研究价值。
<img width="992" height="456" alt="捕获" src="https://github.com/user-attachments/assets/a1cbc7ca-0dfa-41fd-b69d-56e84b773e91" />

## 一句话总结贡献
NeuroLM将 EEG 下游任务从传统“预训练编码器 + 任务分类头微调”转化为“EEG token + 自然语言指令 + 答案生成”的语言模式微调范式，实现了 EEG 任务的统一指令化建模。


## 印象最深刻的点

1. NeuroLM 将 EEG 分类任务转化为自然语言任务描述模型, 改变了 EEG 任务的建模接口和交互方式
2. EEG 信号与自然语言之间天然存在模态差异，直接将 EEG 特征输入语言模型往往会产生表示空间不匹配的问题。NeuroLM 使用 text-aligned neural tokenizer，基于专用classifier 区分 embedding 来自 EEG 还是 text vocab, 通过 adversarial training 让 EEG embedding 在分布上靠近 text embedding space


## 对我们的启发

1. 可以借鉴 NeuroLM 的语言指令微调思想，将 EEG 任务从“分类标签预测”扩展为“任务描述驱动的预测”,可以进一步基于自然语言描述加入更加准确的专家知识,使模型不仅依据信号特征完成分类，还能够结合任务语义和领域先验进行更准确且具解释性的预测
2. 进一步关注 EEG 表征,对齐目标并不局限于文本空间，关键在于构建能够承载任务的有效表征空间：例如，在图像刺激诱发的 EEG 情感识别任务中，EEG 表征更适合与图像特征空间或视觉空间对齐，而非简单映射到自然语言嵌入空间

## Idea是否好想

通用EEG基座模型虽然有很多人做，但是基于指令微调的形式比较新颖。把 EEG 下游任务的适配方式从预训练 EEG encoder + 任务分类头，转成：EEG token + 语言指令 + 答案生成。

## 是否开创性
在 EEG foundation model 领域，开创性比较强。原文明确声称 NeuroLM 是首个利用 LLM 能力、将 EEG 视作外语来实现多任务学习和推理的 EEG 多任务基础模型，并通过 instruction tuning 在单一模型中统一多种 EEG 任务

## 是否属于vision
否

## 是否属于热点
是
## (可选) 其它要补充的

## (可选) 与其它paper的关联
