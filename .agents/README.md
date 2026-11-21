# AI 技能与插件

聊天页整理助手及配套配置集中保存在本目录；仓库中的其他项目各自独立。

## 实际结构

```text
.agents/
├── plugins/
│   ├── marketplace.json
│   └── chat-archive/
│       ├── plugin.json
│       ├── .claude-plugin/plugin.json
│       └── skills/chat-archive/SKILL.md
├── .claude-plugin/marketplace.json
├── README.md
└── skills/github-project-upload/SKILL.md    # 原有的其他独立技能，保持原位
```

唯一的聊天整理规则是 [SKILL.md](plugins/chat-archive/skills/chat-archive/SKILL.md)。规则仍为 v1.4，插件版本为 1.4.0。

## Codex 安装

添加插件市场：来源 `lieying8/codex`，Git 引用 `main`，稀疏路径留空。客户端会读取仓库根目录下的 `.agents/plugins/marketplace.json`，其插件路径为 `./.agents/plugins/chat-archive`。

在 `lieying8-codex` 来源中安装 `chat-archive`，新开聊天并选择聊天页整理助手，再输入“整理本页”“详细整理本页”或“接续本页”。

## Claude Code 安装

为避免在多项目仓库根目录新增 Claude 专属文件，市场清单位于 `.agents/.claude-plugin/marketplace.json`。因此不能再只运行默认的 `claude plugin marketplace add lieying8/codex`。

在 Claude Code 用户设置中的 `extraKnownMarketplaces` 合并下面这一项，保留已有设置：

```json
{
  "extraKnownMarketplaces": {
    "lieying8-codex": {
      "source": {
        "source": "github",
        "repo": "lieying8/codex",
        "ref": "main",
        "path": ".agents/.claude-plugin/marketplace.json"
      }
    }
  }
}
```

再运行 `claude plugin install chat-archive@lieying8-codex`。Claude 市场条目通过标准 `git-subdir` 来源明确指定 `.agents/plugins/chat-archive`，不依赖嵌套市场清单的相对路径解析。

本仓库为私有仓库，客户端需要具备 GitHub 读取权限。当前环境未安装 Claude Code，上述配置依据其官方规范提供，实际安装与调用仍需在目标客户端验证。

## 云端更新规则

以后直接在 GitHub 网页编辑，或在对话里让助手处理。无需下载仓库到 Mac，无需打开终端，也无需用户运行脚本。

- 如果需要修改规则：把修改要求或新版文件交给助手，由助手读取 GitHub 当前版本，修改唯一规则文件并提高通用插件版本。
- 如果已经在 GitHub 网页改好：在对话里说“同步插件配置并提交 GitHub”。
- 助手直接在云端根据通用插件信息生成 Codex 市场清单、Claude 市场清单和 Claude 兼容信息，检查名称、版本和路径一致后提交主分支，并读回核对结果。

唯一规则文件是 `.agents/plugins/chat-archive/skills/chat-archive/SKILL.md`；通用插件信息是 `.agents/plugins/chat-archive/plugin.json`。其他配套配置集中保存在 `.agents`。

目前采用“用户发指令后，由助手云端同步”的方式，尚未配置提交后自动触发。为保持之前约定的目录范围，不新增仓库根级工作流。配套配置由助手在云端按需同步，不再保留需要用户手动执行的同步脚本。

GitHub 中的资料同步完成后，安装插件的 AI 客户端仍需刷新来源并加载新版；已打开的聊天不会仅因 GitHub 更新就自动替换旧规则。

参考：[Agent Plugins](https://agent-plugins.org/)、[Codex 插件](https://developers.openai.com/plugins/build/plugins)、[Claude Code 自定义市场路径](https://code.claude.com/docs/en/plugins/marketplace-reference)。
