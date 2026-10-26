# from_scratch — 用 NumPy 从零实现

不调用任何机器学习框架，用 NumPy 手写核心算法和模型部件。目的是**理解内部机制**，不是造轮子。

| 子目录 | 内容 | 交付周 |
|---|---|---|
| `linear_regression/` | 线性回归：预测、损失、梯度下降、闭式解对照 | 第 4 周 |
| `logistic_regression/` | 逻辑回归 + 多层感知机：激活函数、前向传播、二元分类损失 | 第 5 周 |
| `backpropagation/` | 手写反向传播：计算图、链式法则、梯度检查 | 第 6 周 |
| `attention/` | 最小 scaled dot-product attention | 第 9 周 |

## 统一目录约定

```text
<module>/
├── README.md        # 问题、公式、运行命令、结果、与框架实现的对比
├── requirements.txt # 依赖（通常只有 numpy + pytest）
├── src/             # 核心实现，用 .py 不用 notebook
├── tests/           # 单元测试 / 梯度检查 / 数值对照
├── results/         # 训练曲线、结果表、图表
└── NOTES.md         # 手算过程、形状注释、失败案例
```

## 三条硬性要求

1. **先手算再编码**：至少一个具体数字的小例子，在 `NOTES.md` 里完整写出中间量，然后代码结果必须与之一致。
2. **每个数组都标形状**：关键函数 docstring 里写清输入输出的 shape，例如 `X: (n_samples, n_features) -> y_hat: (n_samples,)`。
3. **必须验证**：
   - 梯度检查（有限差分），相对误差写进 README
   - 与解析解 / 框架实现的对照
   - 至少一个边界输入（空输入、单样本、极端值）

## 顺序约束

严格按 `linear_regression → logistic_regression → backpropagation → attention` 的顺序做。跳步会让梯度检查失去意义——没有第 4 周的闭式解做对照，第 6 周的梯度检查就没有基线。
