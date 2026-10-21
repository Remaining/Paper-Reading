---
title: "ICLR2025 BrainUICL: An Unsupervised Individual Continual Learning Framework for EEG Applications"
date: 2026-10-21
author: qiuyun zhang
---

## 一句话总结内容

传统 EEG 模型在固定数据集上训练完成后参数不再变化，但真实临床/可穿戴应用每天都会出现新的未见受试者。由于生理结构、身体状态等个体差异，固定模型无法持续泛化。作者将真实部署重新建模为“连续到来的个体域”而不是一次性的 target domain。
该场景的核心不是单次域适应，而是 Stability-Plasticity（SP）困境：模型既要对当前新个体具有高 plasticity，又不能因为不断适应而破坏对其他已见/未见个体的 generalization（stability）。
数据被划分为三个互斥受试者集合：labeled source/pretraining set D_S；大量 unlabeled incremental individuals D_T；带标签但只用于评估的 generalization set D_G。
模型 M0 在 D_S 预训练，然后 M0→M1→…→M_NT 逐个适应 D_T 中的新个体；每次适应后都到 D_G 上评估 stability。


## 一句话总结贡献
CL面临的主要挑战是克服稳定性-可塑性（SP）困境，其中可塑性(P)表示模型对新兴个体的适应能力，而稳定性(S)则代表模型对已见过及未见过个体（即新受试者）的泛化能力
研究要使模型既能持续良好地适应多个新出现的个体（更好的 P），又能同时提升对所有未见个体的泛化能力（更好的 S）

## 印象最深刻的点

1. 作者指出三个现实难点：连续个体之间分布差异大，源→目标偏移持续变化；为了适应当前目标而过度 fine-tune 会降低整体稳定性；如果遇到 outlier individual，模型可能发生剧烈性能下降并在后续更新中无法恢复
2. EEG 实际部署更接近“一个人一个域、连续多人到来、目标无真值标签”的 individual-level 问题。考虑到真实场景用户使用中所产生的大量无标签数据使用

## 对我们的启发

1. 可以借鉴 NeuroLM 的语言指令微调思想，将 EEG 任务从“分类标签预测”扩展为“任务描述驱动的预测”,可以进一步基于自然语言描述加入更加准确的专家知识,使模型不仅依据信号特征完成分类，还能够结合任务语义和领域先验进行更准确且具解释性的预测
2. 进一步关注 EEG 表征,对齐目标并不局限于文本空间，关键在于构建能够承载任务的有效表征空间：例如，在图像刺激诱发的 EEG 情感识别任务中，EEG 表征更适合与图像特征空间或视觉空间对齐，而非简单映射到自然语言嵌入空间

## Idea是否好想

通用EEG基座模型虽然有很多人做，但是基于指令微调的形式比较新颖。把 EEG 下游任务的适配方式从预训练 EEG encoder + 任务分类头，转成：EEG token + 语言指令 + 答案生成。

## 是否开创性
在 EEG foundation model 领域，开创性比较强。原文明确声称 NeuroLM 是首个利用 LLM 能力、将 EEG 视作外语来实现多任务学习和推理的 EEG 多任务基础模型，并通过 instruction tuning 在单一模型中统一多种 EEG 任务

## 是否属于vision
是

## 是否属于热点
是
## (可选) 其它要补充的

## (可选) 与其它paper的关联
