# AI 技能与插件

此仓库是公开的插件来源。更新日期 2026-11-23。

| 插件 | 用途 |
| --- | --- |
| [聊天页整理助手](plugins/chat-archive/skills/chat-archive/SKILL.md) | 整理聊天与接续提示 |
| [GitHub 项目上传助手](plugins/github-project-upload/skills/github-project-upload/GUIDE.md) | 上传前审核、精简项目文件和提交验证 |

## Codex 添加源

来源填写 `lieying8/ai`，Git 引用填写 `main`，稀疏路径留空。
刷新来源后，安装 `github-project-upload`，新开聊天选择 GitHub 项目上传助手，再输入“准备上传到 GitHub，先发审核单”。

仓库维护时可从 [上传规则](plugins/github-project-upload/skills/github-project-upload/SKILL.md) 查看审核模板。这里的上传 Skill 仍默认向 `lieying8/codex` 的 `main` 上传项目，具体位置以用户要求为准。

## 目录

```text
.agents/
├── README.md                              插件列表、安装说明和本结构图
├── plugins/
│   ├── marketplace.json                   Codex 插件市场清单
│   ├── chat-archive/                      聊天页整理助手
│   │   ├── plugin.json                    通用插件信息和版本
│   │   ├── .claude-plugin/
│   │   │   └── plugin.json                Claude 兼容插件信息
│   │   └── skills/
│   │       └── chat-archive/
│   │           └── SKILL.md               聊天整理执行规则
│   └── github-project-upload/             GitHub 项目上传助手
│       ├── plugin.json                    通用插件信息和版本
│       ├── .claude-plugin/
│       │   └── plugin.json                Claude 兼容插件信息
│       └── skills/
│           └── github-project-upload/
│               ├── SKILL.md               上传规则和审核模板
│               └── GUIDE.md               使用说明和 Skill 结构图
└── .claude-plugin/
    └── marketplace.json                   Claude 插件市场清单
```

## Claude Code

在用户设置的 extraKnownMarketplaces 中指定此市场文件，保留已有设置：

```json
{"extraKnownMarketplaces":{"lieying8-codex":{"source":{"source":"github","repo":"lieying8/ai","ref":"main","path":".agents/.claude-plugin/marketplace.json"}}}}
```

然后安装 `github-project-upload@lieying8-codex`。已有 chat-archive 条目沿用原配置。
当前来源名称沿用现有的 lieying8-codex，来源地址为 lieying8/ai。

GitHub 更新后客户端需刷新来源并加载插件。仓库文件和清单可核对，客户端安装与调用仍需实际验证。
