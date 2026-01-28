<div align="center">
  <img src="https://img.shields.io/badge/Language-中文-red.svg" alt="中文">
  <img src="https://img.shields.io/badge/Language-English-blue.svg" alt="English">
  <img src="https://img.shields.io/badge/Language-Español-yellow.svg" alt="Español">
  <img src="https://img.shields.io/badge/Language-Português-green.svg" alt="Português">
  <img src="https://img.shields.io/badge/Model-BMSFormer-orange" alt="Model">
  <img src="https://img.shields.io/badge/Task-SOH_Estimation-blueviolet" alt="Task">
  
  <h1>📚 读书笔记：BMSFormer - 面向资源受限BMS的高效SOH估计模型</h1>
  <p>论文：BMSFormer: An efficient deep learning model for online state-of-health estimation of lithium-ion batteries under high-frequency early SOC data with strong correlated single health indicator</p>
  
  <div style="margin: 10px 0;">
    <a href="#readme" style="padding: 5px 10px; background: #333; border-radius: 4px; text-decoration: none; color: #fff; font-weight: bold;">简体中文</a> | 
    <a href="README_en.html" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px; text-decoration: none; color: #333;">English</a> | 
    <a href="README_es.html" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px; text-decoration: none; color: #333;">Español</a> | 
    <a href="README_pt.html" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px; text-decoration: none; color: #333;">Português</a>
  </div>
</div>

> [cite_start]**论文标题**：BMSFormer: An efficient deep learning model for online state-of-health estimation... [cite: 6]  
> [cite_start]**发表期刊**：Energy (2024, Vol.313, 134030) [cite: 2]  
> [cite_start]**核心模型**：BMSFormer (Local-Global Fusion Attention + Depthwise Separable Convolution) [cite: 21, 22]  
> [cite_start]**关键优势**：在计算复杂度大幅降低（线性复杂度）的同时，保持了SOTA级别的预测精度 [cite: 24]。

## 🔍 核心痛点
当前的锂电池 SOH（健康状态）估计面临 "精度" 与 "效率" 难以兼得的困境：
- [cite_start]**传统轻量模型** (如 LSTM, SVM)：计算量小，但在非线性、不稳定数据下精度不足 [cite: 33]。
- [cite_start]**现代深度模型** (如 Transformer, CNNs)：精度高，但依赖复杂的结构和巨大的计算资源，难以在资源受限的 BMS（电池管理系统）嵌入式设备上部署 [cite: 34, 76]。
- [cite_start]**Softmax 瓶颈**：传统 Transformer 的自注意力机制计算复杂度为 $O(N^2)$，对于长序列数据处理极为耗时 [cite: 565]。

## 💡 创新方案：BMSFormer
论文提出了一种轻量级、高效率的深度学习模型 **BMSFormer**。其整体流程包括：高频片段数据获取 -> 特征工程（HI提取） -> 模型训练 -> 评估。

> 📊 **BMSFormer 方法总览图**
> 
> *(此处请插入论文中的 **Fig. 1**: Flowchart of developed SOH estimation approach)*
> ![方法流程图](assets/fig1.jpg)
> [cite_start]*该图展示了从数据获取（Step 1）、特征工程（Step 2）、模型训练（Step 3）到评估（Step 4）的完整闭环。核心在于从高频充放电片段中提取高相关性的健康因子（HIs）。* [cite: 89]

### 核心技术模块
1.  [cite_start]**LGFA 模块 (Local-Global Fusion Attention)**[cite: 21, 530]:
    -   **创新点**：放弃了传统的 Softmax Attention，改用基于 ReLU 的线性注意力机制。
    -   **效果**：将计算复杂度从 $O(N^2)$ 降低到 $O(N)$，大幅提升长序列处理速度。
    -   **融合**：结合了 DSConv-S 模块，增强了对局部特征的敏感度，解决了线性注意力模型表达能力不足的问题。

> 📊 **注意力机制对比图**
> 
> *(此处请插入论文中的 **Fig. 6**: Difference between traditional Softmax... and proposed LGFA)*
> ![注意力机制对比](assets/fig6.jpg)
> [cite_start]*对比图展示了 (a) 传统 Softmax 全局注意力（$O(N^2)$ 复杂度）、(b) 线性注意力 以及 (c) 本文提出的 LGFA 模块。LGFA 通过引入 DSConv-S 实现了线性复杂度的局部与全局特征融合。* [cite: 641]

2.  [cite_start]**多尺度深度可分离卷积 (DSConv)**[cite: 22, 428]:
    -   设计了 **DSConv-S** (小核) 和 **DSConv-L** (大核) 模块。
    -   相比标准卷积，大幅减少了参数量和计算量（FLOPs），同时捕捉多尺度和多通道特征。

> 📊 **BMSFormer 模型架构图**
> 
> *(此处请插入论文中的 **Fig. 4**: Framework of BMSFormer)*
> ![模型架构](assets/fig4.jpg)
> [cite_start]*图示详解了 BMSFormer 的内部结构，包括 LGFA 模块、DSConv-L 模块以及整体的 Block 堆叠方式。* [cite: 480]

## 📈 实验结果与性能
[cite_start]论文在 **Oxford**, **NASA**, **CALCE** 三个主流公开数据集上进行了验证 [cite: 23]。

- [cite_start]**精度提升**：相比 CNN-Transformer, LSTM 等模型，BMSFormer 在 RMSE, MAE, MAPE 等指标上均表现最优，且对突变数据的跟踪能力更强 [cite: 686]。
- **效率惊人**：
    -   [cite_start]训练时间减少约 **21.37%** [cite: 905]。
    -   存储空间占用极低且稳定，适合嵌入式部署。

> 📊 **模型存储空间对比**
> 
> *(此处请插入论文中的 **Fig. 8**: Storage size of five models...)*
> ![存储空间对比](assets/fig8.jpg)
> [cite_start]*该图展示了在不同超参数组合下，BMSFormer (红色) 相比于 CNN-Transformer, LSTM 等模型，始终保持最低且最稳定的存储空间占用。* [cite: 948]

## 📚 参考资料
- **引用格式**: Li, X., Zhao, M., et al. "BMSFormer: An efficient deep learning model for online state-of-health estimation..." Energy 313 (2024): 134030.
- **数据集来源**: Oxford Battery Dataset, NASA Prognostics Repository, CALCE Battery Group.

<br>

<div align="center">
  <p>© 2026 技术博客笔记 | 论文来源：<a href="https://doi.org/10.1016/j.energy.2024.134030">Elsevier Energy</a></p>
  <br>
  <a href="#readme">简体中文</a> | 
  <a href="README_en.html">English</a> | 
  <a href="README_es.html">Español</a> | 
  <a href="README_pt.html">Português</a>
</div>
