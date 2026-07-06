# code-review-claude · Claude-inspired 代码审查 Skill

通用代码审查 Skill，采用 **Claude-inspired 的审查哲学**：先推理 → **对抗式自我验证**（主动推翻每条发现）→ XML 结构化 → 按严重度排序，输出「**少而准**」的高置信度发现。

## 特色
- **失败场景驱动**：每条 bug 写清「触发条件 → 错误结果」，给不出失败场景的不写
- **对抗式验证**：推翻不掉才标 `CONFIRMED`，合理但未坐实标 `PLAUSIBLE`，能推翻的直接丢弃
- **XML 结构化**：内部推理与报告体用 `<finding><evidence><failure><fix>` 分块
- **维度**：正确性 / 安全 / 效率 / 简化复用 / 测试；覆盖广度随 effort 自适应
- 报告模板（Markdown + 零依赖单文件 HTML）见 [`references/report-templates.md`](./references/report-templates.md)

## 开工前会先问（除非你已在指令里给出）
**审查对象**（diff / PR / 目录）· **审查重点** · **报告格式**（Markdown 或单文件 HTML）

## 安装
```bash
git clone https://github.com/0lidaxiang/code-review-claude.git ~/.claude/skills/code-review-claude
```

## 用法
- “用 code-review-claude 审查我当前未提交的改动”
- “帮我 review 这个 PR，重点看正确性和安全”

> 姊妹篇：[`code-review-gpt`](https://github.com/0lidaxiang/code-review-gpt) —— GPT-style 风格（系统化 checklist、逐维度全覆盖、表格化、直接给修复）。同一份代码，两种风格。

## 非官方声明

本项目为个人创作的提示词 Skill，非 Anthropic 或 Claude 官方项目，未获得其背书或授权。

---
*为小红书「RED Skill 大赏」创作 · 标准 `SKILL.md` 格式*
