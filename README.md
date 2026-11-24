# Pneumonia-XRay-Classification
基于 PyTorch 的肺炎 X 光图像分类与可解释性分析

## 📌 项目简介
本项目使用 PyTorch 引入ResNet18，用于识别胸部 X 光片是否患有肺炎。通过处理类别不平衡、引入数据增强以及 Grad-CAM 可解释性分析，完整跑通了医疗图像分类的全流程。

## 🛠️ 环境与依赖
- Python 3.x
- PyTorch, torchvision
- scikit-learn (用于生成分类报告)
- matplotlib, grad-cam (用于可视化)

## 🚀 核心方法与优化
1. **数据增强**：引入随机水平翻转和旋转，缓解因少数类样本（正常图片仅 1341 张）过少导致的过拟合。
2. **类别不平衡处理**：通过给 `CrossEntropyLoss` 赋予 `[3.0, 1.0]` 的权重，重罚模型对“正常”样本的误判，迫使模型学习少数类特征。
3. **多维度评估**：放弃单一的 Accuracy，引入 `classification_report`，重点关注医疗场景下的召回率（Recall），确保不漏诊。

## 📊 实验结果

<img width="1558" height="846" alt="准确率截图" src="https://github.com/user-attachments/assets/55cfc164-7e17-4e3b-855e-7b233834dcdf" />


- **测试集准确率 (Accuracy)**：约 75%
- **肺炎召回率 (Recall)**：约 87%

## 🔬 模型可解释性分析 (Grad-CAM)
<img width="1588" height="782" alt="可解释性截图" src="https://github.com/user-attachments/assets/dfe329d8-d877-42cd-b5dd-751f5174a47b" />


**分析结论**：可视化结果显示，模型的高激活区域主要集中在脊柱、横膈膜以及左上角字母水印处，未能精准聚焦于肺野病灶区。

**反思**：这说明模型在小样本下发生了典型的 **Shortcut Learning（捷径学习）**。

## 🔮 下一步计划
1. 学习并使用 **U-Net** 等图像分割技术，将肺部区域裁剪出来，去除背景干扰。
2. 引入图像注意力机制，引导模型聚焦病灶。
