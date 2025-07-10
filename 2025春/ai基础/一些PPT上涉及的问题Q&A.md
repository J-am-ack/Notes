1. logistic:
   

Logistic Regression 是一种**分类模型**（尤其是二分类），其核心是通过线性模型结合概率映射（Sigmoid函数）实现分类预测。它的三要素如下：

---

### 1. **函数（Function）**
**函数形式**：  
Logistic Regression 的预测函数使用 **Sigmoid函数**（Logistic函数）将线性组合映射到概率区间 `[0, 1]`：  
\[
h(x) = \sigma(w^T x + b) = \frac{1}{1 + e^{-(w^T x + b)}}
\]  
其中：  
- \( w \) 是权重向量，\( b \) 是偏置项，\( x \) 是输入特征。  
- Sigmoid 函数输出可解释为样本属于正类的概率，例如 \( h(x) \ge 0.5 \) 时预测为类别 1，否则为类别 0。

---

### 2. **目标函数（Objective）**
**优化目标**：  
通过**极大似然估计（MLE）**构建损失函数，最小化**交叉熵损失**（Cross-Entropy Loss）：  
\[
J(w, b) = -\frac{1}{N} \sum_{i=1}^N \left[ y_i \log h(x_i) + (1 - y_i) \log (1 - h(x_i)) \right]
\]  
其中：  
- \( N \) 是样本数量，\( y_i \in \{0, 1\} \) 是真实标签。  
- 目标是使预测概率分布与真实标签分布尽可能接近。

**推导逻辑**：  
- 假设样本独立，似然函数为 \( \prod_{i=1}^N h(x_i)^{y_i} (1 - h(x_i))^{1 - y_i} \)。  
- 取负对数似然（转化为最小化问题）即得到交叉熵损失。

---

### 3. **优化方法（Solution）**
**参数求解**：  
由于目标函数是凸函数但无解析解（闭式解），常用**梯度下降法**或改进的优化算法（如拟牛顿法、L-BFGS）迭代求解参数 \( w \) 和 \( b \)。  

**梯度计算**：  
对损失函数 \( J(w, b) \) 求导，梯度为：  
\[
\frac{\partial J}{\partial w} = \frac{1}{N} \sum_{i=1}^N (h(x_i) - y_i) x_i, \quad \frac{\partial J}{\partial b} = \frac{1}{N} \sum_{i=1}^N (h(x_i) - y_i)
\]  
通过梯度更新参数直至收敛：  
\[
w \leftarrow w - \alpha \frac{\partial J}{\partial w}, \quad b \leftarrow b - \alpha \frac{\partial J}{\partial b}
\]  
其中 \( \alpha \) 是学习率。

---

### 总结
| 要素        | 描述                                                                 |
|-------------|----------------------------------------------------------------------|
| **函数**    | 线性组合 + Sigmoid 函数，输出概率值                                   |
| **目标函数**| 交叉熵损失（极大似然估计的负对数形式）                                |
| **优化方法**| 梯度下降等迭代优化算法，无闭式解                                      |

Logistic Regression 是线性分类的基础模型，可通过引入正则化（如 L1/L2）防止过拟合，也可扩展为多分类（如 Softmax Regression）。
2. 