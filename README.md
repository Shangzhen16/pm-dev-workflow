# PM Dev Workflow

A universal Claude Code / Codex skill that helps AI coding agents clarify requirements, plan, build, test, and hand off like product-minded engineers.

一个适用于 **Claude Code / Codex / 其他 AI Coding Agent** 的通用开发工作流 Skill。

它让 AI 在写代码前先像产品经理一样工作：先确认需求、拆清范围、提示风险、制定计划，再开发、自测和交付。

如果你经常遇到 AI 一上来就改代码、做偏需求、漏掉边界情况、交付后不知道怎么测试，这个 Skill 就是为你准备的。

## 一句话说明

把这套 Skill 装进 Claude Code 或 Codex 后，当你说“帮我做一个功能 / 做一个系统 / 改一个需求”时，AI 会自动按下面流程执行：

```text
理解需求 → 判断复杂度 → 澄清关键问题 → 给出产品/技术建议 → 制定开发计划 → 写代码 → 自测 → 给出交付和测试步骤
```

## Before / After

### 不使用这个 Skill

```text
用户：帮我做一个会员支付页面
AI：好的，我开始写代码...
```

常见问题：

- 需求没问清楚
- 不知道用户是谁
- 没有 MVP 范围
- 没有异常状态
- 没有埋点和验收标准
- 交付后用户不知道怎么测试

### 使用这个 Skill

```text
用户：Use $pm-dev-workflow to build a membership payment page.
AI：
1. 先确认目标用户、支付方式、会员权益和成功指标
2. 提醒需要考虑登录态、支付失败、订单状态、退款和埋点
3. 给出 MVP 范围和暂不做内容
4. 制定文件改动和测试计划
5. 开发完成后自测并给出手动验证步骤
```

结果：AI 不只是“写代码”，而是帮你把需求推进成可交付的软件工作。

## Quick Start

1. 把整个文件夹复制到 `~/.claude/skills/` 或 `~/.codex/skills/`
2. 重启一个新的 Claude Code / Codex 会话
3. 开始时直接说：

```text
Use $pm-dev-workflow to help me build...
```

中文也可以：

```text
使用 $pm-dev-workflow 帮我做一个需求，从澄清、计划、开发到测试交付都按流程来。
```

## Why This Exists

Coding agents are fast, but they often jump into code before the requirement is clear. That creates rework, missed edge cases, weak acceptance criteria, and confusing handoffs.

This skill makes the agent behave more like a product-minded engineer:

- clarify the real user/business goal
- separate MVP scope from later ideas
- call out hidden dependencies and risks
- create an implementation plan before editing
- persist context for medium/large work
- self-test before delivery
- explain how a non-technical user can verify the result

## Works With

- **Claude Code**：复制到 `~/.claude/skills/`
- **Codex**：复制到 `~/.codex/skills/`
- **Other AI coding agents**：只要支持读取 `SKILL.md` 指令文件，也可以使用

The core workflow lives in `SKILL.md`. The `agents/openai.yaml` file is optional Codex UI metadata; other agents can ignore it.

## Best For

- 产品经理：让 AI 不再盲目开发，而是先帮你澄清需求和拆范围
- 创业者：把模糊想法变成可以上线的 MVP
- 设计师 / 运营 / 非技术用户：让 AI 给出能看懂、能执行、能测试的交付步骤
- 开发者：在写代码前增加一层轻量产品评审和交付检查

## Good For

- 新功能
- MVP / 试错项目
- 需要先澄清需求的任务
- 需要测试步骤和交付说明的任务

## Not Ideal For

- 只改一个字、一个颜色、一个配置
- 已经完全定好技术方案，只想直接执行
- 不想让 AI 在开发前做任何澄清

## Example Prompts

```text
Use $pm-dev-workflow to build a small dashboard for tracking AI customer-service knowledge-base hit rate.
```

```text
Use $pm-dev-workflow to add a Feed refresh prompt to my mobile H5 prototype.
```

```text
Use $pm-dev-workflow to turn this rough requirement into a scoped MVP and then implement it.
```

## Examples

- [Before / After](examples/before-after.md)
- [Sample feature request](examples/sample-feature-request.md)
- [Sample delivery output](examples/sample-delivery-output.md)

## What The Skill Does

1. 判断需求复杂度：tiny / small / medium / large。
2. 对中大型需求先做产品澄清：目标用户、业务目标、MVP 范围、成功指标、限制条件。
3. 在开发前主动提示风险和建议：登录态、数据结构、埋点、异常状态、技术依赖。
4. 为中大型任务创建 `.dev-context.md`，避免长对话后丢上下文。
5. 开发前给出文件改动范围、执行顺序、风险控制和测试计划。
6. 按确认范围开发，避免随意扩 scope。
7. 开发后先自测：构建、测试、核心路径、空状态、错误状态、权限等。
8. 最后给出清晰交付说明和用户可手动验证的测试路径。

## Install

### Claude Code

```bash
mkdir -p ~/.claude/skills
cp -R pm-dev-workflow ~/.claude/skills/
```

### Codex

```bash
mkdir -p ~/.codex/skills
cp -R pm-dev-workflow ~/.codex/skills/
```


## Repository Structure

```text
pm-dev-workflow/
├── SKILL.md
├── README.md
├── LICENSE
├── examples/
│   ├── before-after.md
│   ├── sample-feature-request.md
│   └── sample-delivery-output.md
└── agents/
    └── openai.yaml
```

## Design Notes

`SKILL.md` 是真正给 AI 读取的核心工作流。README 是给 GitHub 用户看的说明文档。

`agents/openai.yaml` 是 Codex 的可选 UI 元数据。Claude Code 和其他 Agent 可以忽略它。

## Version

v0.1.0

## License

MIT
