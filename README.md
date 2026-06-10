# 🔬 Tumour — 乳腺癌良恶性分类 Machine Learning Project

> 合肥工业大学宣城校区 · 计算机与信息学院 · 电子信息科学与技术专业  
> 机器学习课程大作业 · 2026年5月  
> 作者：宋江琦 | 戴婧婕 | 张子哲 | 张诗雨 | 彭湃

---

## 📌 项目简介

本项目基于 **Kaggle 威斯康星乳腺癌诊断数据集（Wisconsin Breast Cancer Diagnostic Dataset, WBCD）**，系统探索了多种机器学习与深度学习方法在肿瘤良恶性二分类任务中的应用效果。

数据集包含 **569 个样本**和 **30 个**由细胞核图像计算得出的数值特征，分类目标为判断肿瘤是**恶性（Malignant）** 还是 **良性（Benign）**。

我们依次实现并对比了五种主流分类算法：

| # | 模型 | 类型 |
|---|------|------|
| 1 | 逻辑回归 Logistic Regression | 线性模型（基线） |
| 2 | 支持向量机 SVM (RBF核) | 核方法 |
| 3 | 随机森林 Random Forest | 集成学习 |
| 4 | 全连接神经网络 FCNN | 深度学习 |
| 5 | 梯度提升树 XGBoost | 集成学习 |

---

## 📊 实验结果

| 模型 | Accuracy | Precision | Recall | F1-Score |
|------|----------|-----------|--------|----------|
| 逻辑回归 | 0.9737 | 0.9756 | 0.9524 | 0.9639 |
| SVM | 0.9737 | 0.9756 | 0.9524 | 0.9639 |
| 随机森林 | 0.9561 | 0.9744 | 0.9048 | 0.9383 |
| **FCNN** ⭐ | **0.9912** | **1.0000** | **0.9767** | **0.9882** |
| XGBoost | 0.9737 | 1.0000 | 0.9286 | 0.9630 |

> 在医疗诊断场景中，**召回率（Recall）** 是最关键的指标——漏诊一例恶性肿瘤的代价远高于误报。FCNN 以 97.67% 的召回率在五种模型中表现最佳。

---

## 📁 文件结构

```
Tumour/
├── data.csv          # 威斯康星乳腺癌诊断数据集
├── tumour.ipynb      # 主实验 Notebook（含完整代码与分析）
├── tumour.html       # Notebook 的 HTML 导出版本（便于预览）
└── 输出图片.zip       # 所有可视化图表（共18张）
```

---

## 🗂️ 数据集说明

- **来源**：UCI Machine Learning Repository / Kaggle
- **样本数**：569（良性 357 条 / 恶性 212 条，比例约 6:4）
- **特征数**：30个数值型特征，由细胞核图像的10种物理属性（半径、纹理、周长、面积、平滑度、紧凑度、凹度、凹点数、对称性、分形维度）× 3种统计量（均值、标准误差、极值）计算得出
- **标签**：`diagnosis`（M→1 恶性，B→0 良性）

---

## 🔧 实验流程

### 1. 数据清洗与探索（EDA）
- 删除无关列（`id`、`Unnamed: 32`）
- 类别分布可视化，确认良恶性比例约 6:4，无需过采样
- 相关系数热力图，识别并剔除高共线性特征（阈值 0.9），特征从30维压缩至约20维
- T检验计算各特征的类别区分度，筛选最强/最弱区分特征并可视化

### 2. 数据预处理
- **Z-score 标准化**（StandardScaler）：消除量纲差异
- **数据集划分**：训练集 60% / 验证集 20% / 测试集 20%（stratify 保证比例一致）

### 3. 模型训练与评估
每种模型均评估以下四项指标：
- **Accuracy**（准确率）
- **Precision**（精确率）
- **Recall**（召回率）⬅ 医疗场景最关键指标
- **F1-Score**（调和平均）

### 4. 特征压缩对比实验
对比 30维 vs 20维 特征数据集在逻辑回归上的表现，验证冗余特征剔除的合理性。

---

## 📈 可视化输出（部分）

| 图表 | 说明 |
|------|------|
| 肿瘤类型分布图 | 类别均衡性检验 |
| 相关系数热力图 | 特征共线性分析 |
| 小提琴图 & KDE密度图 | 最强/最弱特征的类别区分度 |
| 逻辑回归训练曲线 | Loss 收敛过程 |
| FCNN 训练/验证 Loss 曲线 | 过拟合检测 |
| 混淆矩阵（各模型） | 分类误差详情 |
| ROC 曲线（各模型） | AUC 综合区分能力 |
| 特征重要性排名（随机森林 / XGBoost） | 诊断价值最高的特征 |

---

## 🛠️ 环境依赖

```bash
pip install numpy pandas matplotlib seaborn scikit-learn xgboost torch scipy
```

| 库 | 用途 |
|----|------|
| `numpy` / `pandas` | 数据处理 |
| `matplotlib` / `seaborn` | 数据可视化 |
| `scikit-learn` | 逻辑回归、SVM、随机森林、数据预处理 |
| `xgboost` | XGBoost 模型 |
| `torch` (PyTorch) | 全连接神经网络 FCNN |
| `scipy` | T检验（特征区分度分析） |

---

## 🚀 快速开始

```bash
# 1. 克隆仓库
git clone https://github.com/Vandom-Z/Tumour.git
cd Tumour

# 2. 安装依赖
pip install numpy pandas matplotlib seaborn scikit-learn xgboost torch scipy

# 3. 运行 Notebook
jupyter notebook tumour.ipynb
```

也可以直接打开 `tumour.html` 在浏览器中预览完整的实验过程和所有输出图表，**无需安装任何环境**。

---

## 🔍 关键结论

1. **FCNN 综合性能最佳**（Accuracy 99.1%，Recall 97.67%），得益于 BatchNorm + Dropout + Early Stopping 的正则化组合，在小样本下有效避免了过拟合。
2. **XGBoost 精确率达 100%**（零误报），适合对误报容忍度低的场景；但召回率相对偏低，临床应用需权衡。
3. **特征压缩有效**：约 1/3 的特征高度冗余，剔除后模型性能基本持平，说明合理降维可以简化模型、提升鲁棒性。
4. **逻辑回归不可忽视**：在该线性近似可分的结构化数据上，简单的逻辑回归已能达到 97.4% 准确率，是中小型医疗数据集的可靠基准方案。

---

## 📚 参考资料

- [UCI Machine Learning Repository - Breast Cancer Wisconsin (Diagnostic)](https://archive.ics.uci.edu/ml/datasets/Breast+Cancer+Wisconsin+(Diagnostic))
- [Kaggle - Breast Cancer Wisconsin (Diagnostic) Data Set](https://www.kaggle.com/datasets/uciml/breast-cancer-wisconsin-data)
- Scikit-learn Documentation: https://scikit-learn.org
- XGBoost Documentation: https://xgboost.readthedocs.io

---

*合肥工业大学宣城校区 · 2026年5月*
