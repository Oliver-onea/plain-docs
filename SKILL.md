---
name: plain-docs
description: Turn any technical project into plain-language documentation that non-engineers can actually understand. Use when the user asks to "解释项目/写通俗文档/给新人讲懂/写导读/write plain-language docs/make an explainer/onboarding doc"，or when project docs exist but people outside the team can't understand them. Produces a layered doc set (plain guide → diagrams → one-pager) using analogy-first writing, jargon decoding, and honest capability boundaries. Tool-agnostic: works via any agent that can read this file and a codebase.
metadata:
  version: "1.0.1"
  date: "2026-08-19"
  license: MIT
  repo: https://github.com/Oliver-onea/plain-docs
---

# plain-docs：把技术项目写成外行能懂的文档

把任何代码仓库/技术系统，变成一份**完全没接触过的人 10 分钟能读懂**的导读文档。
核心方法：**类比先行、黑话解码、诚实边界**——不是简化版说明书，是翻译。

## 何时使用

- 用户说「看不懂现有文档」「写个通俗版」「给新人/老板/跨部门讲懂这个项目」
- 项目文档齐全但全是工程师黑话，外面的人读不进去
- 需要一页纸向上汇报或对外介绍

## SOP：六步法（严格按序执行）

### Step 1 · 一句话心智模型（最难也最重要）

用「它是一个 ___ 的 ___」句式给项目定性，必须包含：
- 一个日常生活的身份（工具/职业/场所）
- 一个它独有的执着点（本项目特有的原则）

写不出来说明你还没懂这个项目，回去重读代码，不许往下走。

**例**：它是一个「网上资料采集器」——你给主题，它把相关网页原文**原封不动**抓回来存档+记账。（"原封不动"就是它的执着点：不做分析，分析归下游）

### Step 2 · 生活化类比通篇

为系统找一个**完整的职业类比**（图书采购员、海关、翻译官、图书馆……），然后把系统的每个模块映射到这个职业的一个动作上。

规则：
- 类比必须是**一个职业的完整工作流**，不是零散比喻（采购员的"找线索→取货→登记→回访"，而不是东一个西一个的比喻）
- 一个模块一个动作，一一对应，画成两列对照
- 类比只用于结构和流程；**数字、约束、边界必须回到技术事实**

### Step 3 · 黑话解码表

扫描项目文档/代码里的高频术语（frontier、idempotent、fencing token 这类），做一张表：

| 术语 | 人话（≤15 字） |
|---|---|
| frontier | 待办队列数据库 |

规则：每条人话必须**独立成立**（不出现"就像""类似于"），且不许损失关键语义——"待办队列数据库"比"一个队列"好，因为 frontier 确实持久化。

### Step 4 · 图的逐行翻译

如果项目有架构图/流程图，外行看图还是不懂。把图里**每一个框、每一条边**翻译成人话，做成「左边原图元素、右边人话」的对照表。图不再是自解释的，靠这张表解释。

### Step 5 · 诚实的能/不能清单

两张清单，**每条"能"都必须有实证**（实测数据、跑过的记录），每条"不能"都要写清是「边界」（设计上就不做）还是「还没做」（ roadmap 项）。不许把"还没做"写成"不做"，不许把没测过的写成能。

这是这份文档建立信任的核心——读者（尤其决策者）最需要的不是"它很强"，是"它到底几斤几两"。

### Step 6 · 去哪下一步

最后一张导览表：读者读完这份之后，想动手/想深入/想看契约，分别去哪个文件。让导读成为入口，而不是终点。

## 产出契约

三件套（放 `docs/`，别堆仓库根目录）：

| 文件 | 角色 | 长度 |
|---|---|---|
| `PROJECT_GUIDE.md` | 人话导读（本 SOP 的成品）| ≤120 行 |
| `PROJECT_DIAGRAM.md` | ASCII 图示版 | ≤200 行 |
| `PROJECT_ONE_PAGER.md` | 密度版一页纸（数字全可溯源）| ≤60 行 |

每份打上文档治理 tag（type/authority/scope/conflict-resolution），互相声明权威关系（导读 defer to README/CONTRACT），防止和正式文档打架。

## 质量红线（自查）

1. 找一个真外行（或模拟）读 Step 1 那句话——复述不出项目是干嘛的，就重写
2. 类比表里不许出现任何未解码的黑话
3. 「能」清单里每条都能指着一个实测证据
4. 全文搜"简单来说"“显而易见”——出现即删，那是偷懒不是解释
5. 三个文件读的顺序 GUIDE→DIAGRAM→ONE_PAGER，每层信息增量清晰

## 反面案例（不要这样做）

- ❌ 「简单来说，frontier 就是一个队列」→ 丢了持久化语义，且"简单来说"是偷懒
- ❌ 类比混用：一半说图书馆一半说工厂 → 读者脑内模型崩塌
- ❌ 「支持分布式」写在能力清单里但从未实施过 → 信任破产
- ❌ 把导读写成功能列表的堆砌 → 那是 README，不是导读
