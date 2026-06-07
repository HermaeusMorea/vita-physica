# Vita Physica 构想笔记

Vita Physica is a running universe whose inhabitants learn to name its physics.

这份笔记保存项目最初讨论中浮现出的核心想法。它还不是正式 spec，而是这个项目的概念种子。

## 核心直觉

Vita Physica 是一个 agent 时代的生命游戏。

它的重点不是让 agent 直接控制细胞、动作或世界状态，而是让一个底层宇宙持续运行；与此同时，agent 在运行过程中观察这个宇宙，提取高层对象，发明描述它们的语言，提出语义物理法则，验证这些法则，并把通过验证的对象类型和法则安装进更高的组织阶。

一句话：

```text
kernel 运行宇宙
agent 在其上演化物理学
```

## 底层物理

kernel 拥有细粒度的 runtime reality。

在传统生命游戏中，这就是 cell 层面的规则系统：

```text
B3/S23
死细胞周围正好有 3 个活邻居时诞生
活细胞周围有 2 或 3 个活邻居时继续存活
否则死亡或保持空白
```

kernel 不理解 glider、oscillator、signal、colony 或 computation。它只是按照已安装的底层动力学推进宇宙。

kernel rules 是现实的 substrate。它们不是普通运行时旋钮。如果底层规则改变了，等于宇宙本身改变了。

## 语义物理

高层语义物理由粗粒度规则组成，用来描述从细粒度 kernel dynamics 中涌现出的稳定结构。

例子：

```text
still life 保持不变
oscillator 会在某个周期后回到原形
一个 glider 每 4 个细粒度 tick 沿对角线移动一次
gun 会周期性发射 moving pattern
collision 会转化、湮灭或发射 pattern
```

这些法则不覆盖 kernel。它们让 kernel universe 在高层变得可理解。

一条粗粒度规则只有在其声明的组织阶下与更细粒度的动力学相容时才有效。

核心相容性形状是：

```text
project(fine_evolve(state, k)) == coarse_evolve(project(state))
```

也就是说：先让细粒度状态演化再投影，应该等于先投影到粗粒度对象再应用粗粒度规则。

## 组织阶

组织阶（organization order）不是普通显示界面，也不是一层 UI。

组织阶是世界在某一尺度上形成可读对象和可验证法则的方式。它回答的是：
在这一尺度上，什么东西可以被当作对象？这些对象有哪些状态？它们如何交互？
它们如何由低阶对象组成？它们又如何成为更高阶对象的材料？

一个组织阶定义：

```text
projection：如何从低阶 states 或 traces 识别高阶对象
object types：这一阶有哪些对象类型
state variables：这些对象有哪些可追踪状态
relations / interactions：这些对象之间有什么关系和交互
composition rules：低阶对象如何组成这一阶对象
laws：这一阶对象如何演化
validity conditions：这些法则在什么条件下成立
compatibility obligations：这一阶法则如何与下阶动力学相容
```

组织阶可以用 `O0, O1, O2...` 标识。编号是稳定的内部坐标；语义别名可以随着
宇宙的发现逐渐长出来。例如在一个类生命游戏宇宙中，早期可能出现这样的直觉：

```text
O0: substrate / cells
O1: local forms
O2: stable bodies
O3: assemblies
O4: systems
```

这些名字不是永久分类。真正重要的是：每一阶都有自己的对象、状态、交互、
组合和法则。当一阶足够稳定，它又会成为更高组织阶的 substrate。

组织阶是高层对象变得可运行的地方：

```text
cell soup
-> recurring shape
-> stable body
-> body assembly
-> functional system
```

每一阶语言都会让更高阶现象变得可发现。

## Agents

agent 不应该直接命令 runtime behavior。

agent 参与的是规则系统的演化：

```text
观察
猜想
命名
提案
验证
安装
使用
审计
细化
```

agent 可以注意到反复出现的结构，提出新的对象类型，提出粗粒度法则，建议新的组织阶，或者细化已有语义规则。

但 agent proposal 不是现实。它只是 candidate。

## Verifier / Experiment Layer

verifier 是语义物理的实验层和证明层。

它检查 agent 提出的高层法则是否与下层动力学相容，是否与已经安装的语义规则相容。

可能的证明层级：

```text
Tier 0：经验样本
Tier 1：有限窗口穷举检查
Tier 2：SAT / SMT 无反例搜索
Tier 3：model checking 或 invariant proof
Tier 4：proof assistant theorem，例如 Lean / Coq / Isabelle
```

这一层类似 Lean 之于数学，只是它要证明的对象不是普通数学定理，而是 semantic-physics laws。

一条 proposed law 可以从 observed regularity 开始，随着证据和证明增强，逐渐升级为更强的、可安装的语义物理法则。

## 规则演化

高层语义物理可以演化。

演化可以包括：

```text
新增对象类型
新增 pattern identity
新增 interaction law
新增 organization-order projection
规则细化
规则限制
规则废弃
跨 semantic epoch 的 migration
```

已安装的语义法则应该是 append-only 或 epoch-based 的。失败或被替代的法则不应从历史中抹除，而应被替换、缩小适用域，或标记为 obsolete。

anomaly 很重要。如果一条粗粒度法则预测失败，kernel history 不会被改写。anomaly 是细化语义物理的证据。

## 底层规则与 Genesis

改变底层 kernel rules 是宇宙级事件，不是普通运行时操作。

如果 kernel dynamics 改变，大多数高层语义物理都必须被 invalidated、revalidated、migrated，或者被 quarantine 在旧 kernel hash 之下。

因此，更干净的设计是：

```text
Genesis / universe design：
  寻找有趣的底层动力学和初始 life 分布

Runtime / semantic physics：
  冻结一个 kernel universe，让 agent 在其中演化高层物理学
```

初始 life 分布很重要，因为它决定一次 run 的宇宙历史实际暴露哪些现象。kernel rule 决定什么法则在原则上可能存在；初始分布决定这段历史中哪些法则会被看见、命名、验证和安装。

## 设计句子

```text
Kernel physics makes the world run.
Semantic physics makes the world mean.
```

或者：

```text
宇宙持续演化。
它的居民学习命名自己的物理学。
```
