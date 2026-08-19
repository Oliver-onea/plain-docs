# Example: turning a web crawler codebase into plain docs

This is a real worked example of the plain-docs SOP, so you can see what
"done" looks like at each step.

## Project context (input)

A 48k-line Python "collection layer" repo: takes a topic profile, discovers
candidate URLs (Google News / DuckDuckGo / RSS), crawls them with a durable
SQLite-backed engine (leases, robots compliance, per-origin politeness,
topic gate, asset filtering), archives raw bytes content-addressed, emits an
audit trail. Downstream repos do extraction and mining.

## Step 1 output — one-sentence mental model

> **它是一个「网上资料采集器」：你告诉它一个主题，它去网上把相关网页的原文原封不动抓回来存档，并记录每次抓取的完整来龙去脉。**

The insistence point: **原封不动** (verbatim) — it does no analysis; analysis
belongs to downstream layers. That one word carries the repo's core boundary.

## Step 2 output — the professional analogy

Chosen identity: **a very rule-abiding book procurement agent** (特别守规矩的图书采购员).

| System module | Agent's action |
|---|---|
| topics.json | the purchase order you hand them |
| discovery layer | scouting channels for leads |
| frontier scheduling | queue numbers; no crowding, no repeats, retry on failure |
| robots compliance | reading the door notice; never entering where forbidden |
| adaptive throttle | pacing; no burst-firing at one site |
| topic gate | door check: off-topic page? not queued. |
| asset filter | images/CSS are "not material", discarded |
| egress proxies | sometimes entering through a different gate (IP rotation) |
| raw-archive + events | numbering and logging every acquired item |
| recrawl | scheduling return visits |

Rules honored: one profession, one complete workflow, every module mapped.
Numbers and constraints stay technical (e.g. "RFC 9309" stays, but the table
above explains *what it's for*).

## Step 3 output — jargon decoder (excerpt)

| 术语 | 人话 |
|---|---|
| frontier | 待办队列数据库 |
| topic gate | 主题门卫：无关链接拒收 |
| raw-archive | 原文证据库：带指纹、谁也改不了 |
| 归因三元组 | 每份资料的出生证明 |
| egress/代理池 | 出口管理：换 IP 防拉黑 |
| recrawl | 定期回访排期 |

Each gloss stands alone, none drop key semantics.

## Step 4 output — translating a diagram, line by line

The journey-of-one-crawl diagram had steps like `② frontier 调度 → topic
gate ✋ → ③ robots → ④ egress → ⑤ 三路 transport`. The decoder table maps
every box: 采购员排队取号 → 门口检查 → 看门口告示 → 决定从哪个门进 →
三种方式取货(普通/伪装指纹/真开浏览器).

## Step 5 output — honest capability list (excerpt)

能（都实测过）：
- 按主题抓取（中英文），单轮上千页；1430 篇实测，归因 100%
- 静态/JS 渲染/PDF 都能抓

不能 / 还没做：
- 不做内容分析（边界：设计如此，归下游）
- 撞到 captcha 页面还不认识（**还没做**：Phase 1 后半，设计已定稿）
- 多机分布式（**还没做**：设计定稿未实施）

Note the boundary-vs-not-yet distinction on every "cannot".

## Step 6 output — where-to-next table

| 你想… | 去哪 |
|---|---|
| 跑一次采集 | README「运行」节 |
| 看数据契约 | docs/CONTRACT.md |
| 看引擎内部 | docs/runtime-internals.md |
| 看图（工程师视角）| docs/PROJECT_DIAGRAM.md |

## Final artifacts

Three files, governed with doc-tags, reading order GUIDE → DIAGRAM →
ONE_PAGER. The GUIDE (plain-language, ≤120 lines) is the entry point; the
ONE_PAGER keeps every number traceable to a source.
