# ml-learning-lab — 机器学习与 AI 长期学习实验室

> 把 AI 当作学习导师和研究协作者，而不是答案生成器。
> 通过「独立思考 → 原理推导 → 动手实现 → 实验验证 → 复盘沉淀」的闭环，逐步建立可以迁移到新论文、新模型和新开源项目上的能力。

**长期路线、阶段状态与验收标准见 [`LEARNING_PLAN.md`](LEARNING_PLAN.md)。本文件只做仓库导航与运行说明。**

- 默认节奏：每周 5–8 小时
- 当前阶段：阶段 0（基线与环境），详见 `LEARNING_PLAN.md` §13.1 状态表

| 项 | 值 |
|---|---|
| 本地路径 | `/home/lie/studyProject/ml-learning-lab` |
| 远程仓库 | `https://github.com/zhenglieAllen/ml-learning-lab.git` |

---

## 目录结构

```text
ml-learning-lab/
├── LEARNING_PLAN.md          # 长期路线、阶段状态、验收标准
├── README.md                 # 仓库目标、运行方式、索引（本文件）
├── journal/
│   ├── weekly/                # 每周复盘
│   └── sessions/              # 单次学习记录
├── foundations/
│   ├── math/                  # 线性代数、微积分、概率统计
│   └── ml/                    # 经典机器学习
├── from_scratch/
│   ├── linear_regression/
│   ├── logistic_regression/
│   ├── backpropagation/
│   └── attention/
├── pytorch_lab/               # PyTorch 练习和测试
├── papers/
│   └── <paper-name>/          # 论文笔记、复现实验、结论
├── repos/                     # 第三方源码阅读笔记，不必复制完整仓库
├── experiments/
│   └── <experiment-name>/     # 配置、结果、日志、图表
├── mistakes/                  # 常见误解、调试记录和复习卡片
└── projects/                  # 阶段性综合项目
```

---

## 各目录职责

| 目录 | 存放内容 | 什么时候写入 |
|---|---|---|
| `journal/sessions/` | 单次学习记录（模板见 `LEARNING_PLAN.md` §7） | 每完成一个主题的学习闭环 |
| `journal/weekly/` | 每周复盘（模板见 `LEARNING_PLAN.md` §12） | 周末，依据实际证据更新状态 |
| `foundations/` | 数学与经典 ML 的长期知识笔记 | 通过推导和验证之后 |
| `from_scratch/` | 用 NumPy 从零实现的算法/模型部件 | 基础阶段的核心交付物 |
| `pytorch_lab/` | PyTorch 练习、框架对照与自动微分实验 | 从 NumPy 版本迁移到框架时 |
| `papers/` | 单篇论文的结构化笔记与复现记录 | 精读论文时 |
| `repos/` | 第三方仓库的源码阅读笔记与调用链图 | 追踪开源项目时 |
| `experiments/` | 完整实验的配置、日志、结果表、图表 | 做对照/消融实验时 |
| `mistakes/` | 常见误解、调试记录、复习卡片 | 发现自己判断错误时（当天记录） |
| `projects/` | 阶段性综合项目 | 阶段末的综合交付 |

---

## 运行方式

### 环境

推荐使用 `uv` 或 `venv`，在仓库根目录创建独立虚拟环境：

```bash
# uv
uv venv && source .venv/bin/activate && uv pip install numpy matplotlib pytest

# 或标准 venv
python3 -m venv .venv && source .venv/bin/activate && pip install numpy matplotlib pytest
```

Python 版本建议 3.10+。实际使用的版本与依赖请记录在每个实验目录的 `README.md` 中。

### 目录约定

每个可独立运行的子项目采用统一布局：

```text
<project>/
├── README.md      # 问题、运行命令、环境、验收标准
├── requirements.txt
├── src/ 或 *.py  # 核心逻辑，尽量是 .py 而不是全部塞进 notebook
├── tests/         # 单元测试 / 梯度检查 / 数值对照
└── results/       # 日志、结果表、图表
```

### 常用命令

```bash
pytest                    # 运行全部测试
python -m pytest tests/  # 运行指定目录
python script.py --seed 0 # 显式传种子，便于复现
```

### 可复现性要求

固定随机种子只是第一步。每次实验同时记录：

- Python 版本、框架与关键依赖版本
- 数据来源、版本与切分方式
- 随机种子、超参数、批大小、训练步数
- 设备与硬件信息
- **从干净环境运行的完整命令**

---

## 索引

### 学习进度

- 阶段状态表：`LEARNING_PLAN.md` §13.1
- 主题状态取值：`未开始` / `进行中` / `待复习` / `已通过`

### 常用模板

| 模板 | 位置 |
|---|---|
| 主题学习记录 | `LEARNING_PLAN.md` §7 |
| 论文阅读 | `LEARNING_PLAN.md` §8 |
| 源码阅读 | `LEARNING_PLAN.md` §9 |
| 实验规范 | `LEARNING_PLAN.md` §10 |
| 每周复盘 | `LEARNING_PLAN.md` §12 |

### 当前内容

| 路径 | 说明 | 状态 |
|---|---|---|
| `journal/sessions/00-baseline.md` | 阶段 0 基线自测 | 待完成 |
| `foundations/math/` | 线性代数、微积分、概率统计 | 未开始 |
| `foundations/ml/` | 经典机器学习 | 未开始 |
| `from_scratch/linear_regression/` | NumPy 线性回归 | 未开始 |
| `from_scratch/logistic_regression/` | NumPy 逻辑回归 | 未开始 |
| `from_scratch/backpropagation/` | 手写反向传播与梯度检查 | 未开始 |
| `from_scratch/attention/` | 最小 scaled dot-product attention | 未开始 |
| `pytorch_lab/autograd/` | 自动微分与框架对照 | 未开始 |
| `papers/attention-is-all-you-need/` | Transformer 原始论文精读 | 未开始 |
| `projects/pretrained-model-baseline/` | 预训练模型基线 | 未开始 |
| `projects/final-project/` | 阶段性综合项目 | 未开始 |

---

## 学习闭环

每个主题都按同一流程执行，一次只推进一个知识点：

1. **提出问题** —— 明确本次要回答的一个问题
2. **先独立作答** —— 先写出自己的理解，即使不完整也保留
3. **逐步讲解** —— 让 AI 用提问和提示引导，而不是直接给答案
4. **推导与实现** —— 先讲清数学，再写最小实现；先 NumPy
5. **验证与反例** —— 数值测试、梯度检查、边界输入
6. **复述与迁移** —— 关掉原文用自己的话重讲，并解决一个变体问题
7. **沉淀** —— 记录结论、误解、证据、代码入口和下一步问题

**通过标准不是「看完 / 跑通」，而是能解释、能推导、能实现、能验证中的至少三项（核心基础主题要求全部四项）。**

详细的 AI 导师行为规则与可直接复制的启动提示词见 `LEARNING_PLAN.md` §2。

---

## 提交规范

- 按主题或实验拆分 commit，避免一个巨大 notebook 长期累积
- 提交信息说明「做了什么」和「验证方式」
- 失败实验和错误理解**保留**，它们是知识资产
- 关键逻辑抽成 `.py` 并配测试；notebook 只用于探索、可视化和过程记录
