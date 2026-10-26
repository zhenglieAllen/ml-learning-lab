# from_scratch/attention — 最小 Scaled Dot-Product Attention

**交付周**：第 9 周（注意力机制）

## 要解决的问题

从序列建模的痛点出发理解注意力，用 NumPy 实现最小的 scaled dot-product attention，再用 PyTorch 验证。

## 必须自己回答的问题

- 序列建模的痛点是什么？RNN 的梯度消失和顺序依赖是具体什么问题？
- Query / Key / Value 各自的直觉含义是什么？分别对应输入的哪一部分？
- `Q @ K.T` 得到的是什么？每一行、每一列的含义？
- 为什么要除以 `sqrt(d_k)`？不除会怎样（数值上 + 训练上分别说明）？
- softmax 在哪一步作用？掩码（mask）是什么，为什么需要？

## 公式

```text
Attention(Q, K, V) = softmax(Q @ K.T / sqrt(d_k) + M) @ V
```

写出每个符号的含义与形状：

| 符号 | 含义 | 形状 |
|---|---|---|
| Q | query | `(batch, seq_len, d_k)` |
| K | key | `(batch, seq_len, d_k)` |
| V | value | `(batch, seq_len, d_v)` |
| `Q @ K.T` | 相似度分数 | `(batch, seq_len, seq_len)` |
| 输出 | 加权求和结果 | `(batch, seq_len, d_v)` |

## 实现清单

- [ ] `attention(Q, K, V)` —— NumPy 版本
- [ ] 支持 causal mask（只看当前位置及之前）
- [ ] 形状断言在代码里写死
- [ ] PyTorch 对照版本（→ `pytorch_lab/`）

## 验证要求

| 检查 | 期望 |
|---|---|
| 手算例子 | 至少 3 个：全 0 输入、单点全 1、随机小矩阵，逐值核对 |
| 形状测试 | 至少 3 个（`LEARNING_PLAN.md` 明确要求） |
| softmax 行和为 1 | 每行和 ≈ 1.0 |
| 掩码正确性 | 被掩位置权重 ≈ 0 |
| 与 PyTorch 对照 | 数值差异 < 1e-6 |

## 交付物

`src/` + `tests/`（≥3 个测试）+ `NOTES.md`（数值例子与形状注释）+ `README.md`

## 常见错误

- 缩放因子用了 `sqrt(d_model)` 而不是 `sqrt(d_k)`
- 掩码用 `-inf` 但在 softmax **之后**才加（应该是加在 logits 上）
- Q/K/V 维度顺序搞反，或把 batch 维当成了序列维
- 用 `np.matmul` 时 `(seq, d) @ (seq, d)` 得到的是逐元素乘积而非矩阵乘
