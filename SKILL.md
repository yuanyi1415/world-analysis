---
name: world-analysis
description: >
  世界分析法。用于复杂问题、理论、架构、分类模型、重大决策与冻结前验证。
  自动从七种分析方法中选择最小充分组合：第一性约简、对抗性约简、双向钢人、
  正交性分析、不变量与极端反例、外部证据校核、最小实证。
  当用户要求“用世界分析法分析/验证/攻击/推演/判断/冻结”，或当前任务明显需要
  本质分析、模型约简、竞争方案对撞、结构正交检查、系统性证伪、外部证据验证、
  真实实验验证时使用。
---

# 世界分析法

版本：v1.0.0

## 1. 目标

世界分析法不是七个 Prompt 的合集，也不是固定七步 Workflow。

它是一套通用分析与验证协议：

> **针对当前问题，选择最小充分的方法组合，发现本质、攻击假设、校核证据，并形成可继续推进或可冻结的结论。**

默认原则：

```text
先明确要判断什么
↓
选择最少必要方法
↓
按方法原生协议执行
↓
仅在结果触发下一方法时继续
↓
形成统一 Verdict
```

禁止默认把七种方法全部执行一遍。

---

## 2. 七种方法

| 编号 | 方法 | 核心问题 | Reference |
|---|---|---|---|
| 01 | 第一性约简 | 去掉现成答案后，最少什么必须成立？ | `references/01_第一性约简.md` |
| 02 | 对抗性约简 | 当前模型里什么可以删、并、解耦？ | `references/02_对抗性约简.md` |
| 03 | 双向钢人 | 当前主张与最强竞争解释，谁更站得住？ | `references/03_双向钢人.md` |
| 04 | 正交性分析 | 当前分类是否把不同语义维度混在一起？ | `references/04_正交性分析.md` |
| 05 | 不变量与极端反例 | 什么必须始终成立，什么最容易击穿它？ | `references/05_不变量与极端反例.md` |
| 06 | 外部证据校核 | 外部世界真正证明了当前 Claim 的哪一部分？ | `references/06_外部证据校核.md` |
| 07 | 最小实证 | 最低成本做什么，才能获得足以改变决策的真实证据？ | `references/07_最小实证.md` |

**渐进加载要求：**
- 先用本文件完成路由。
- 只读取本轮真正需要的方法 Reference。
- 只有发生明确方法衔接时，才继续读取下一份 Reference。
- 不因“可能有用”而预加载全部七份材料。

---

## 3. Analysis Target

执行前先把用户问题归一为一个明确 Analysis Target。

至少确认：

```text
Target
当前真正要分析 / 判断 / 验证什么？

Scope
这次结论影响到什么边界？

Known Facts
哪些事实已经确认？

Constraints / Commitments
哪些约束不能随意改变？

Current State
当前是否已有候选模型、主张、方案或实验结果？
```

如果信息已经足够，直接分析。

只有缺失信息会实质改变方法选择或结论时，才询问最少必要问题；否则基于当前材料继续，并显式标注关键假设。

---

## 4. Method Router

### 4.1 第一性约简

优先选择，当问题属于：

- 新领域 / 新本体 / 新核心概念；
- “这个东西本质是什么”；
- 怀疑已有术语绑架设计；
- 模型已经复杂到需要回到底层语义；
- 争议来自基本假设不一致。

典型信号：

```text
到底需不需要这个 Entity？
本质是什么？
最小不可替代的是什么？
去掉现有架构重新想。
```

---

### 4.2 对抗性约简

优先选择，当：

- 已经存在候选模型；
- Entity / State / Layer / Type 持续膨胀；
- 怀疑过度设计；
- 多个概念边界相近；
- 准备冻结前需要压缩结构。

典型动作：

```text
Delete
Merge
Decoupling Split
Local Counterexample Check
```

若 `Decoupling Split` 是否成立仍不清楚，转 04 正交性分析。

---

### 4.3 双向钢人

优先选择，当：

- 存在明确重大取舍；
- 有 A / B 两种竞争路线；
- 当前共识可能存在确认偏误；
- 需要比较当前主张与真正最强的替代解释。

不要机械生成反命题；必须寻找 `Strongest Material Rival`。

若 Verdict 为 `Insufficient Evidence`：
- 外部事实或成熟实践可解决 → 转 06。
- 当前场景必须实测才能解决 → 转 07。

---

### 4.4 正交性分析

优先选择，当：

- 分类、状态、等级模型疑似混维；
- 一个对象经常同时属于多个“互斥类型”；
- 单轴枚举不断增长；
- 对抗性约简发现潜在 `Decoupling Split`。

核心判断：

```text
Question Test
Variation Test
Constraint Test
Value Test
```

不要因为“逻辑上能拆”就拆；拆分必须降低真实耦合或提高解释力。

---

### 4.5 不变量与极端反例

优先选择，当：

- 需要验证一个 Claim / Model 是否真的扛得住；
- 准备冻结核心理论；
- 结论含“始终 / 必须 / 绝不”；
- 生命周期、可靠性、权限、安全、恢复等边界重要。

覆盖：

```text
Material Assumptions
Material Dependencies
Core Invariants
```

目标是寻找最小合法击穿条件，不是无限枚举异常场景。

若 Verdict 为 `Insufficient Evidence`：
- 外部证据可确认 → 转 06。
- 必须真实执行才能确认 → 转 07。

---

### 4.6 外部证据校核

优先选择，当：

- 需要验证成熟理论 / 产品 / 工程实践；
- 怀疑闭门推演；
- 用户明确要求“外部找背书 / 查成熟案例 / 验证”；
- 03 或 05 因缺少外部事实无法继续。

必须同时：

```text
Search Support
+
Search Strongest Material Counterevidence
```

证据按 `Evidence Fit` 判断，不按来源数量或名气投票。

若 Verdict 为 `Inconclusive` 且本地实验可解决 → 转 07。

如果当前 Runtime 没有外部检索能力：
- 不得伪造外部证据；
- 明确标记该方法未实际执行；
- 可仅输出 Evidence Needs / Search Plan。

---

### 4.7 最小实证

优先选择，当：

- 理论推演已无法区分方案；
- 性能、成本、稳定性、真实用户效果必须实测；
- 外部证据无法决定当前场景；
- 需要判断某项复杂能力是否值得产品化。

目标是：

> `Minimum Decision-Sufficient Experiment`

不是 Demo，也不是绝对成本最小实验。

如果当前 Runtime 没有执行、测试或真实数据能力：
- 不得声称已完成实证；
- 只设计实验与判定标准；
- 明确状态为 `Empirical Test Pending`。

---

## 5. 最小充分方法集

默认只执行能够推动当前判断的最少方法。

### 新模型 / 新理论

常见组合：

```text
01 第一性约简
→ 02 对抗性约简
→ [04 正交性分析，仅当存在混维问题]
→ 05 不变量与极端反例
→ [06 外部证据校核，重大冻结或需要外部背书时]
```

不是强制流水线。若某一步没有新增价值，跳过。

### 已有模型疑似过度设计

```text
02 对抗性约简
→ [04 正交性分析]
→ 05 不变量与极端反例
```

### 重大方案取舍

```text
03 双向钢人
→ [06 外部证据校核]
→ [07 最小实证]
```

只有上一步无法合理区分时才进入下一步。

### 冻结前验证

根据风险选择：

```text
02 对抗性约简
+
05 不变量与极端反例
+
[06 外部证据校核]
```

涉及分类混维时加 04。

### 单一明确方法请求

用户明确说“用第一性约简”“做双向钢人”等：

- 优先按用户指定方法执行；
- 不自动追加其他方法；
- 只有指定方法自身 Verdict 明确要求下一步，或缺少下一方法会造成伪结论时，才追加并说明原因。

---

## 6. Method Handoff

方法之间只有出现明确触发条件才衔接。

```text
01 第一性约简
→ 产出 Candidate Model
→ 若需要削减结构：02

02 对抗性约简
→ 发现 Decoupling Split 候选
→ 04

03 双向钢人
→ Insufficient Evidence
→ 06 或 07

04 正交性分析
→ 产出 Recompose
→ 必要时回 02 检查最小充分性

05 不变量与极端反例
→ Boundary Found / Model Defect
→ 回到对应建模方法修正
→ Insufficient Evidence
→ 06 或 07

06 外部证据校核
→ Challenged / Reframed / Narrowed
→ 回到原模型修正
→ Inconclusive
→ 07（若可实证）

07 最小实证
→ Conditional
→ 修正 Claim / Scope
→ Non-discriminating
→ 重设计实验或返回分析层
```

禁止为了“流程完整”强行继续。

---

## 7. 统一 Verdict Contract

每个方法保留其原生 Verdict，不统一改写。

最终综合输出使用统一 Envelope：

```text
Conclusion
当前最重要结论

Methods Used
本轮实际使用了哪些方法，以及为什么

Key Findings
真正改变判断的 2～5 个发现

Native Verdicts
各方法原生 Verdict

Open Assumptions / Evidence Gaps
仍未解决的关键假设或证据缺口

Overall Status
Proceed
Conditional
Revise
Evidence Needed
Empirical Test Pending

Freeze Readiness
Ready
Ready with Scope
Not Ready
```

### Overall Status

- `Proceed`：当前结论足以继续下一阶段。
- `Conditional`：结论依赖明确条件，必须带 Scope 使用。
- `Revise`：模型存在实质缺陷，应先修正。
- `Evidence Needed`：缺少决定性事实或外部证据。
- `Empirical Test Pending`：需要真实实验才能判断。

### Freeze Readiness

`Ready` 只在：
- 关键语义已明确；
- 当前模型没有已知实质缺陷；
- 决定性反例已处理；
- 没有会改变结论的关键证据缺口。

`Ready with Scope`：
- 结论稳定，但仅在明确边界内成立。

`Not Ready`：
- 仍存在 Model Defect、关键冲突、关键证据缺口或待实证变量。

禁止使用没有依据的数字“可信度评分”。

---

## 8. Freeze Protocol

当用户要求“验证后冻结”“是否可以冻结”时：

1. 先明确本轮要冻结的 Claim / Model / Scope。
2. 不默认重跑全部七种方法。
3. 至少选择一个**结构攻击**或**证伪方法**：
   - 02 对抗性约简，或
   - 05 不变量与极端反例。
4. 对重大、外部可验证的理论边界，优先追加 06。
5. 如果关键结论取决于当前真实运行效果，必须转 07；仅靠语言推演不得冻结为“已实证”。
6. 最终明确：
   - 冻结内容；
   - 适用 Scope；
   - 未冻结内容；
   - 重新打开条件。

冻结表示：

> **在没有新证据前作为后续事实基准。**

不表示永久真理。

---

## 9. 全局分析纪律

### 9.1 先结论，后关键理由

默认输出：

```text
结论
↓
2～5 个关键发现
↓
必要反例 / 条件
↓
Verdict / Freeze Readiness
```

不默认输出完整思维流水账。

### 9.2 不制造确定性

允许：

```text
Conditional
Insufficient Evidence
Inconclusive
Non-discriminating
Not Ready
```

不得为了“回答完整”强迫明确胜负。

### 9.3 不虚构权重与阈值

未经用户、业务规则、冻结目标、SLA、Baseline 或真实证据支持，不得自行编造：

- 评价权重；
- 风险分数；
- Decision Threshold；
- 可信度百分比。

### 9.4 术语不是事实

已有名词、成熟产品结构、历史实现和行业惯例只能是：

> 候选解释 / 外部证据 / 当前约束

不能自动成为第一性事实。

### 9.5 案例不是权威

外部成熟实践用于验证机制与边界，不用于复制表象。

### 9.6 最小 ≠ 极简

所有 Reduction 都必须同时满足：

```text
Minimum
+
Sufficient
```

### 9.7 分析能力与工具能力分离

如果当前环境无法搜索、运行实验、读取真实系统状态：

- 明确说明未执行哪一步；
- 输出可执行的 Evidence Need / Experiment Design；
- 不把设计结果伪装成真实验证结果。

---

## 10. Reference Loading Rules

只在选中某方法时读取对应完整 Reference：

```text
01 → references/01_第一性约简.md
02 → references/02_对抗性约简.md
03 → references/03_双向钢人.md
04 → references/04_正交性分析.md
05 → references/05_不变量与极端反例.md
06 → references/06_外部证据校核.md
07 → references/07_最小实证.md
```

Reference 中的：

- 定义；
- 适用边界；
- 核心动作；
- 停止条件；
- 原生 Verdict；
- 硬约束；

均为该方法的正式事实源。

SKILL.md 只负责：

> **路由、组合、衔接和统一输出。**

若 SKILL.md 与 Reference 出现语义冲突：

> **以对应方法 Reference 为准，并标记需要修订 Skill 整合层。**

---

## 11. 默认输出模板

```text
【结论】
一句话给出当前判断。

【使用的方法】
- 方法：为什么本轮需要它

【关键发现】
1.
2.
3.

【关键边界 / 反例】
- ...

【Native Verdict】
- 方法 A：...
- 方法 B：...

【仍未解决】
- ...

【Overall Status】
Proceed / Conditional / Revise / Evidence Needed / Empirical Test Pending

【Freeze Readiness】
Ready / Ready with Scope / Not Ready
```

简单问题可以进一步压缩，不要求机械输出所有栏目。

---

## 12. 核心原则

世界分析法最终遵循：

> **先找本质，再建模型；先攻击模型，再相信模型；先确认外部证据证明了什么，再引用案例；只有真实观测能够决定的问题，才进入实证。**

以及：

> **选择最少的方法，获得足够的判断。**

Skill 的成功标准不是“分析得最多”，而是：

> **以尽可能少的分析复杂度，形成经得起反例、证据和真实世界检验的最小充分结论。**
