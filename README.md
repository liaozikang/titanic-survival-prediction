# titanic-survival-prediction
zikang'first try on machine learining
# Titanic Survival Prediction

[Kaggle Competition](https://www.kaggle.com/c/titanic) | Python | Scikit-learn

## 📌 项目简介

基于 Titanic 乘客数据（船舱等级、性别、年龄、兄弟姐妹数量、父母子女数量、票价、登船港）预测其在沉船事故中是否生还。本项目实现了一个完整的机器学习 pipeline，包括数据预处理、特征编码、标准化、随机森林模型训练，最终在 Kaggle 公开排行榜上获得 **0.765** 的准确率。

## 📁 数据集

- `train.csv`：训练集，包含标签 `Survived`
- `test.csv`：测试集，不含标签，用于提交预测结果
- 来源：Kaggle Titanic 竞赛

## 🔧 方法

### 特征工程（当前版本）

使用以下原始特征（未进行高级特征衍生）：
- 数值型：`Pclass`, `Age`, `SibSp`, `Parch`, `Fare`
- 分类型：`Sex`, `Embarked`

### 预处理流程

- **数值特征**：缺失值用中位数填充，然后标准化（`StandardScaler`）
- **类别特征**：缺失值用众数填充，然后进行 One‑Hot 编码（`OneHotEncoder`，设置 `handle_unknown='ignore'` 以处理测试集中可能出现的新类别）
- 整个预处理使用 `ColumnTransformer` 与 `Pipeline` 封装，避免数据泄露，并支持交叉验证

### 模型

- **随机森林分类器** (`RandomForestClassifier`)
  - `n_estimators = 200`
  - `random_state = 42`
- 其他参数保持默认

## 📈 结果

- **交叉验证准确率**（训练集划分验证）：约 0.82
- **Kaggle 公开排行榜得分**：**0.765**

> 注：当前版本仅使用了原始特征，未进行特征工程优化（如提取称呼、家庭规模、票价分组等），仍有较大提升空间。

## 🚀 如何运行

1. 克隆本仓库
2. 确保安装依赖：`pip install pandas scikit-learn`
3. 下载数据集（或直接从 Kaggle 读取）
4. 运行 `titanic.ipynb` 或 `titanic.py`

```bash
python titanic.py
