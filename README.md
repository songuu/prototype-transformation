# prototype-transformation

前端文档流水线 Claude Code 插件 — 将原型图 + 原始需求文字，经过四个阶段逐步增强为可直接指导开发的完整前端文档。

## 流程

```text
原始需求文字 + 原型图
        ↓
阶段2  原型解析   →  初始文档 (requirements-v1)
        ↓  ⛔ 人工确认
阶段3  Figma挂载  →  中间文档 (requirements-v2)
        ↓  ⛔ 人工确认
阶段4  接口集成   →  接口文档 (requirements-v3)
        ↓  ⛔ 人工确认
阶段5  代码审计   →  审计报告 (audit-report)
        ↓  ⛔ 人工确认
开发实现
```

每个阶段产出后需人工确认，确认后才进入下一阶段。

## 模型分工

| 角色 | 模型 | 负责阶段 |
| --- | --- | --- |
| 主持人 | Sonnet 4.6 | 协调全局、阶段3执行 |
| 分析者 | Opus 4.6 | 阶段2原型分析、阶段4接口绑定 |
| 挑刺者 | gpt-5.3-codex xhigh | 阶段2/4文档质量审查 |
| 终审者 | gpt-5.3-codex high | 阶段5代码审计 |

## 安装

```bash
claude plugin add ./prototype-transformation
```

## 使用

在 Claude Code 中直接触发：

- 提供原型图 + 需求文字 → 自动进入阶段2
- 说"挂 Figma 链接" → 进入阶段3
- 说"绑定接口文档" → 进入阶段4
- 说"审计代码" → 进入阶段5

## 目录结构

```text
prototype-transformation/
├── .claude-plugin/
│   └── marketplace.json
├── README.md
└── plugins/
    └── prototype-transformation/
        ├── .claude-plugin/
        │   └── plugin.json
        └── skills/
            └── doc-pipeline/
                ├── SKILL.md
                ├── evals.json
                └── references/
                    ├── Codex调用协议.md
                    ├── 阶段2-原型解析.md
                    ├── 阶段3-Figma挂载.md
                    ├── 阶段4-接口集成.md
                    └── 阶段5-代码审计.md
```

## 作者

[songuu](https://github.com/songuu)
