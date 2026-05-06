# 易宇社区数学框架与技术规范

本文档为易宇社区的研究与开发奠定数学基础，定义关键概念与计算规范。

## 📐 核心数学符号与定义

### 基本对象

| 符号 | 定义 | 备注 |
|------|------|------|
| $Y$ | 易（阴阳二元系统）| 基础对偶对 |
| $Y_i$ | 五行（木火土金水） | $i \in \{1,2,3,4,5\}$ |
| $G_{jk}$ | 八卦 | $j, k \in \{0,1\}^3$ |
| $\phi(t)$ | 太极场势 | 时空函数 |
| $\mathcal{T}$ | 时间周期 | $\{\tau_L, \tau_M, \tau_S\}$ |
| $\rho(x,t)$ | 能量密度 | 位置与时间的函数 |

### 易宇观公理

**公理 1（二元性）**
任何自然现象都可用 $Y = \{0, 1\}$ 的对偶表示（阴/阳）。

**公理 2（五行结构）**
五行形成循环生克关系：
$$\text{木} \to \text{火} \to \text{土} \to \text{金} \to \text{水} \to \text{木}$$

**公理 3（八卦完备性）**
八卦系统 $\{G_{jk}\}$ 是所有现象的完备分类。

**公理 4（太极场）**
存在标量场 $\phi(x,t)$ 满足：
$$\nabla^2 \phi - \frac{1}{c^2}\frac{\partial^2 \phi}{\partial t^2} = -4\pi \rho(x,t)$$

---

## 🔄 周期理论

### 大中小"三周期"定义

$$\tau_L > \tau_M > \tau_S$$

**大周期** $\tau_L$：
- 定义：4860 年（天文学基础）
- 应用：文明周期、宇宙尺度事件
- 公式：$\tau_L = 2^8 \times 19 = 4860$

**中周期** $\tau_M$：
- 定义：约 60 年（干支周期）
- 应用：气候、经济、社会周期
- 公式：$\tau_M \approx 60 \times k$（$k$ 为适应指数）

**小周期** $\tau_S$：
- 定义：日、月、年等自然周期
- 应用：日常预测、短期变化
- 公式：$\tau_S = \{1 \text{ day}, 27.3 \text{ days}, 365.25 \text{ days}, ...\}$

### 多尺度时间框架

对于时间序列 $x(t)$，定义多尺度分解：

$$x(t) = \sum_{i} A_i \cos(2\pi f_i t + \phi_i) + \epsilon(t)$$

其中频率 $f_i$ 对应各周期：
$$f_i \in \left\{\frac{1}{\tau_L}, \frac{1}{\tau_M}, \frac{1}{\tau_S}\right\}$$

---

## ⚡ 太极场方程

### 方程形式

$$\boxed{\nabla^2 \phi(x,t) = -\rho(x,t)}$$

与 Poisson 方程对标。

### 解的表示

Green 函数解：
$$\phi(x,t) = \int \frac{\rho(x',t)}{4\pi |x-x'|} dx'$$

### 边界条件

- **Dirichlet 型**：$\phi|_{\partial \Omega} = f$
- **Neumann 型**：$\nabla \phi \cdot n|_{\partial \Omega} = g$
- **周期型**：用于全局场

---

## 🧬 易学符号的数学表示

### 二元表示（阴阳）

```
阳 = +1  或  1  或  ──  (连线)
阴 = -1  或  0  或  ⚌⚌  (断线)
```

向量表示：$\vec{Y} = (y_1, y_2, ..., y_n)$，其中 $y_i \in \{-1, +1\}$

### 五行矩阵

生克关系可用矩阵表示：

$$M = \begin{pmatrix}
0 & 1 & 0 & 0 & -1 \\
-1 & 0 & 1 & 0 & 0 \\
0 & -1 & 0 & 1 & 0 \\
0 & 0 & -1 & 0 & 1 \\
1 & 0 & 0 & -1 & 0
\end{pmatrix}$$

其中：
- $M_{ij} = 1$：第 $i$ 行生第 $j$ 行
- $M_{ij} = -1$：第 $i$ 行克第 $j$ 行
- $M_{ij} = 0$：无直接关系

### 八卦映射

8 个八卦对应 $\mathbb{Z}_2^3$ 中的 8 个元素：

| 八卦 | 符号 | 二进制 | 含义 |
|------|------|--------|------|
| 乾 | ☰ | 111 | 天（纯阳） |
| 坤 | ☷ | 000 | 地（纯阴） |
| 震 | ☳ | 100 | 雷（动） |
| 艮 | ☶ | 001 | 山（止） |
| 坎 | ☵ | 010 | 水（流） |
| 离 | ☲ | 101 | 火（明） |
| 兑 | ☱ | 011 | 泽（喜） |
| 巽 | ☴ | 110 | 风（入） |

---

## 📊 预测模型规范

### 时间序列分解

任何可观测量 $X(t)$ 可分解：

$$X(t) = T(t) + S(t) + \epsilon(t)$$

其中：
- $T(t)$：趋势分量（多项式或样条）
- $S(t)$：季节分量（周期函数的叠加）
- $\epsilon(t)$：残差（白噪声）

### 周期识别算法

**方法 1：傅里叶变换**

$$\hat{f}(k) = \sum_{t=0}^{N-1} X(t) e^{-2\pi i kt/N}$$

功率谱：$P(k) = |\hat{f}(k)|^2$

**方法 2：自相关函数**

$$\rho(\tau) = \frac{\sum_t (X(t) - \bar{X})(X(t+\tau) - \bar{X})}{\sigma^2 N}$$

周期出现在 $\rho(\tau)$ 的峰值处。

### 预测精度指标

| 指标 | 定义 | 范围 |
|------|------|------|
| MAE  | $\frac{1}{n}\sum \|y_i - \hat{y}_i\|$ | $[0, \infty)$ |
| RMSE | $\sqrt{\frac{1}{n}\sum (y_i - \hat{y}_i)^2}$ | $[0, \infty)$ |
| MAPE | $\frac{1}{n}\sum \frac{\|y_i - \hat{y}_i\|}{y_i} \times 100\%$ | $[0, \infty)$ |
| R²   | $1 - \frac{\sum(y_i - \hat{y}_i)^2}{\sum(y_i - \bar{y})^2}$ | $(-\infty, 1]$ |

---

## 🤖 AI 实现规范

### 数据预处理

```python
# 标准化
X_normalized = (X - mean(X)) / std(X)

# 对数变换（若必要）
X_log = log(X + ε)

# 分割：训练/验证/测试 = 70:15:15
```

### 模型架构建议

**基础模型**：LSTM 或 Transformer

```python
model = Sequential([
    LSTM(64, return_sequences=True, input_shape=(time_steps, features)),
    Dropout(0.2),
    LSTM(32),
    Dense(16, activation='relu'),
    Dense(output_size, activation='linear')
])
model.compile(optimizer='adam', loss='mse', metrics=['mae'])
```

**易宇专用编码**：

```python
# 易学符号编码
def encode_yijing(state):
    # 将八卦/五行状态转为向量
    mapping = {'乾': [1,1,1], '坤': [0,0,0], ...}
    return mapping[state]

# 周期特征
def extract_period_features(X, periods=[60, 365.25, 4860]):
    features = []
    for p in periods:
        features.append(FFT_magnitude_at_frequency(1/p))
    return features
```

---

## 📈 验证方法

### 回测（Backtesting）

对于历史数据进行后验验证：

1. **分割数据**：(过去数据) | (预测数据) | (验证数据)
2. **训练模型**：在过去数据上
3. **预测**：预测数据部分
4. **对标**：与实际验证数据比较

### 前向验证（Out-of-sample）

对未来数据进行预测验证：

1. **冻结模型**：在某个时间点停止更新
2. **预测未来**：基于过去数据
3. **等待真实数据出现**
4. **计算误差**

---

## 🔬 技术栈推荐

### 数学与科学计算

```python
# 基础库
import numpy as np
import scipy as sp
import pandas as pd

# 时间序列
from statsmodels.tsa import seasonal, stattools
from tslearn import metrics

# 傅里叶分析
from scipy.fft import fft, fftfreq
import pywt  # 小波变换
```

### 机器学习与深度学习

```python
# TensorFlow / PyTorch
import tensorflow as tf
from tensorflow.keras import layers

import torch
import torch.nn as nn

# 自动机器学习
from auto_sklearn.regression import AutoSklearnRegressor
```

### 可视化

```python
import matplotlib.pyplot as plt
import plotly.graph_objects as go
import seaborn as sns
```

---

## 📝 计算报告模板

所有计算结果应包含：

```markdown
## [项目名称]

### 问题陈述
明确研究问题

### 数学模型
给出（简要）数学表述

### 算法与实现
1. 使用的方法
2. 代码位置
3. 计算资源

### 实验结果
- 数值结果（表格）
- 可视化（图表）
- 性能指标

### 讨论
- 结果的含义
- 与已知方法的对比
- 局限性与改进方向

### 参考文献
相关白皮书与论文
```

---

## ✅ 验证清单

提交任何计算结果前，确保：

- [ ] 数学推导是正确的
- [ ] 代码已测试并可复现
- [ ] 结果有物理或应用意义
- [ ] 误差与不确定性已评估
- [ ] 文档清晰完整

---

## 💡 常见问题

**Q: 如何处理缺失数据？**
A: 使用插值（线性、样条、KNN）或删除小段缺失。对于大段缺失，需要特殊处理。

**Q: 为什么我的预测精度很低？**
A: 检查：
1. 数据质量与完整性
2. 周期识别是否正确
3. 模型是否收敛
4. 是否存在非平稳性

**Q: 如何中西融合验证？**
A: 保持双轨制：一方面用传统统计学，另一方面用易宇模型，比较结果。

---

## 参考

- `gitee/yi-yu-whitepaper/易宇观公理体系：东方科学范式的数学根基.md`
- `gitee/yi-yu-whitepaper/东方系统科学计算范式：从太极场方程到可验证的计算路径.md`
- `gitee/yi-yu-whitepaper/易宇观・大中小周期定义.md`

---

**最后更新**：2024年

**贡献者**：易宇社区数学与技术工作组
