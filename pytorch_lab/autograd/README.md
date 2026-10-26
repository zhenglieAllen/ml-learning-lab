# pytorch_lab/autograd — 自动微分与框架对照

**交付周**：第 7 周（自动微分与 PyTorch）

## 要解决的问题

理解 PyTorch 的自动微分在背后做了什么，并用一个**通过的梯度对照测试**证明自己手写的 NumPy 反向传播和框架一致。

## 三件事

1. **读懂一个小型自动微分引擎**
   建议 [micrograd](https://github.com/karpathy/micrograd)：先理解单个标量节点（`Value` 类、`__mul__` / `__add__` / `__pow__`、`backward()`），再追踪一个完整的训练迭代。
   产出：关键代码路径图（哪个文件哪个函数做什么），放在 `NOTES.md`。

2. **自己画一遍计算图**
   对一个具体表达式手写前向顺序和反向顺序，说明梯度在图上是怎么回流的。

3. **逐项对照手写 NumPy 版本**
   用 `from_scratch/backpropagation/` 的实现作为基准，对比 PyTorch。

## 必做对照测试

```text
同一组参数与输入
  → NumPy 前向输出  vs  PyTorch 前向输出
  → NumPy 梯度      vs  PyTorch 梯度
  → 一步更新后的参数
```

全部要求逐元素一致（相对误差 < 1e-5）。

## 必答问题

- `.grad` 是什么时候被填充的？`retain_graph=True` 解决什么问题？
- 为什么 PyTorch 默认累加梯度而不是覆盖？
- `optimizer.step()` 到底做了什么（是它算梯度，还是 PyTorch 的 `backward()` 算的）？
- `loss.backward()` 和 `loss.backward(retain_graph=True)` 的区别？
- `torch.autograd.grad` 和 `.backward()` 的区别，什么时候用哪个？

## 交付物

- `NOTES.md` —— micrograd 关键代码路径图 + 手画计算图
- `src/` —— PyTorch 对照实现
- `tests/` —— 梯度对照测试（关键交付物）
- `README.md` —— 结论与框架和手写实现的差异说明

## 常见错误

- `zero_grad()` 调用位置错误
- 用了 `.data` 或 `.detach()` 意外切断了计算图
- 在 `no_grad` 上下文里做反向
- 叶子节点（leaf tensor）上直接做需要梯度的运算，报错信息被忽略
