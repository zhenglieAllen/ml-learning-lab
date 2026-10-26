# pytorch_lab — PyTorch 练习与对照

从 NumPy 版本迁移到框架，学习 PyTorch 的自动微分、模块化、训练流程。这一层的目的是**理解框架在替你做什么**，而不是熟练调 API。

| 子目录 | 内容 | 交付周 |
|---|---|---|
| `autograd/` | 自动微分引擎原理、`backward()` / `zero_grad()` / 优化器行为、与手写 NumPy 版本的逐项对照 | 第 7 周 |

## 计划覆盖

- 第 7 周：阅读一个小型自动微分引擎，理解计算图、梯度累积、`backward()`、`zero_grad()`、优化器行为；研究 [micrograd](https://github.com/karpathy/micrograd)；用 PyTorch 重做一个小模型并与手写版本对照损失和梯度。
- 第 8 周：训练可靠性与泛化 —— mini-batch、SGD/Adam、学习率、权重衰减、Dropout、早停、模型选择；走一遍官方 PyTorch 初学者流程（数据加载 → 建模 → 训练 → 保存 → 推理）。

## 必做对照实验

PyTorch 版本和 NumPy 版本**必须逐项对比**，而不是只看最终 loss 接近：

| 对照项 | 期望 |
|---|---|
| 同一输入的前向输出 | 逐元素一致 |
| 同一参数的梯度 | 逐元素一致（相对误差 < 1e-5） |
| 一步更新后的参数 | 一致 |
| 完整训练曲线 | 高度重合 |

## 必答问题

- `backward()` 之后梯度存在哪？`.grad` 属性是什么？
- 忘记 `zero_grad()` 会发生什么？为什么 PyTorch 默认**不**帮你清零？
- `optimizer.zero_grad()`、`model.zero_grad()`、`set_to_none=True` 三者区别？
- `with torch.no_grad():` 和 `eval()` 分别解决什么问题（一个管梯度，一个管 BN/Dropout）？
- `requires_grad_()` 什么时候需要手动打开？
- 同样的 seed，PyTorch 和 NumPy 结果不完全一致是为什么？

## 目录约定

```text
<module>/
├── README.md
├── requirements.txt
├── src/ or *.py
├── tests/
└── results/
```

## 常见错误

- 训练循环里 `zero_grad()` 位置放错（在 `backward()` 之后清零 → 少更新一步）
- `model.train()` / `model.eval()` 没切换，评估时 Dropout 仍在随机丢弃
- 用 `.item()` 在训练循环里同步，拖慢训练
- 训练集和评估集用同一个 `Dataset` 对象而没打乱/洗牌切分
- `device` 不一致导致 tensor 混用 CPU/GPU 报错
