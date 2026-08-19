# plain-docs (skill)

把任何技术项目写成**外行 10 分钟能读懂**的文档——一个 Claude Code / opencode 通用的 Agent Skill。

不是"简化版说明书"，是**翻译**：类比先行、黑话解码、诚实边界。

## 它解决什么

工程师写的项目文档，外面的人（新同事、老板、跨部门、客户）读不进去：
满屏黑话、图不自解释、能力吹嘘没有实证。plain-docs 用一套六步 SOP
强制产出三层可读文档：

| 产物 | 角色 |
|---|---|
| `PROJECT_GUIDE.md` | 人话导读（入口）——一句话心智模型 + 职业类比 + 黑话解码表 |
| `PROJECT_DIAGRAM.md` | 图示版——架构图的逐行人话翻译 |
| `PROJECT_ONE_PAGER.md` | 密度版一页纸——每个数字可溯源 |

## 六步 SOP（详见 SKILL.md）

1. **一句话心智模型**——「它是一个 ___ 的 ___」，必须带项目的执着点
2. **职业类比通篇**——一个职业的完整工作流映射所有模块，不许比喻混用
3. **黑话解码表**——每条人话独立成立、不丢关键语义
4. **图逐行翻译**——每个框每条边配人话对照
5. **诚实能/不能清单**——每条"能"有实证；区分"边界（不做）"和"还没做"
6. **去哪下一步**——导读是入口不是终点

## 安装

```bash
# Claude Code
git clone https://github.com/Oliver-onea/plain-docs ~/.claude/skills/plain-docs

# opencode（项目级）
git clone https://github.com/Oliver-onea/plain-docs .opencode/skill/plain-docs
```

装好即用：对 agent 说「用 plain-docs 把这个项目写成人话」或直接
「给我写个通俗版项目导读」，skill 的 description 会自动触发。

## 使用

在目标项目根目录对 agent 说：

> 用 plain-docs skill，给这个仓库写一套通俗文档

Agent 会读仓库 → 按六步 SOP 产出三件套到 `docs/` → 每份带治理 tag。

## 实战样例

见 [references/example.md](references/example.md)：一个 4.8 万行爬虫仓库
怎么被翻译成"特别守规矩的图书采购员"——含每一步的真实产出。

## License

MIT
