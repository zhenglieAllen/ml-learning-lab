# sessions — 单次学习记录

每完成一个主题的完整闭环（提问 → 独立思考 → 推导 → 实现 → 验证 → 复述 → 沉淀），在这里新增一份记录。

## 命名

`NN-topic-slug.md`，`NN` 为顺序编号，保证文件按学习顺序排列：

```text
00-baseline.md
01-linear-algebra.md
02-calculus-probability.md
03-classical-ml-loop.md
04-logistic-regression-mlp.md
05-backpropagation.md
06-autograd-pytorch.md
07-training-generalization.md
08-attention.md
09-transformer-paper.md
10-min-transformer.md
11-huggingface-baseline.md
12-finetune-eval.md
```

## 每份记录必须包含

按 `LEARNING_PLAN.md` §7 的模板，五个部分都要填：

1. **学习前：独立思考** —— 不查资料的原始回答与预测
2. **核心理解** —— 一句话解释、关键公式与符号、成立条件、我的错误
3. **实现与验证** —— 代码路径、运行命令、预期 vs 实际、反例
4. **验收** —— 四个勾选项（解释 / 推导 / 实现 / 验证）
5. **复盘与下一步** —— 掌握什么、仍不清楚什么、下次最小行动

## 注意

- 不要在事后补写第 1 节。补写的「独立思考」没有价值。
- 第 4 节未勾满就不要把该主题标为「已通过」。
- session 中发现的错误理解，同步一条到 `mistakes/`。
