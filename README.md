# 学习笔记 Skill · 思源知识组织规范

把源码、手册、调试经历、文章和对话整理成给人阅读的中文学习笔记。先讲原理、因果和例子，让半年后的自己仍能理解和应用；源码与检索过程不占据正文。

这个仓库同时提供学习笔记写作方法和思源工具使用规范。它适合创建笔记、综合知识、规划笔记分工与关联；用户仅要求指导时，只生成指导，不自动重组已有笔记。

## 从这里开始

| 入口 | 解决的问题 |
| --- | --- |
| [SKILL.md](skills/learning-notes/SKILL.md) | 从材料中提炼什么，以及怎样写成人能理解的解释 |
| [知识库长期维护](skills/learning-notes/references/knowledge-maintenance.md) | 页面变多后如何按生命周期维护、分库、导航、拆分和归档 |
| [思源知识组织与工具规范](skills/learning-notes/references/siyuan-conventions.md) | 主笔记分工、减少重复、标签、双链、关系图及各种工具的职责 |
| [两个思源 MCP](skills/learning-notes/references/siyuan-mcp.md) | Sisyphus 与官方 MCP 的能力路由、原生结构写入和读回 |
| [视觉设计](skills/learning-notes/references/visual-design.md) | 标题、提示、图表、超级块，以及 Obsidian / HTML 设计的适配 |
| [写法与示例](skills/learning-notes/references/writing-examples.md) | 因果解释、知识综合、数字例子与完稿判断 |
| [AGENTS.md](AGENTS.md) | 可放入项目或转为思源指导笔记的简短 AI 入口 |
| [来源与取舍](skills/learning-notes/references/sources.md) | 检查过的参考材料、吸收的方法和未迁移的约束 |

## 安装与使用

下载或克隆本仓库，将 `skills/learning-notes` 整个文件夹复制到所用客户端的 Skill 目录。Windows 下 Codex 可放在 `%USERPROFILE%\.codex\skills\learning-notes`；使用 `.agents/skills` 的环境可放到 `%USERPROFILE%\.agents\skills\learning-notes`。目录已存在时先比较内容，再按本仓库同步；不要把仓库根目录的 `AGENTS.md` 当成 Skill 文件复制进去。

如需 `.agent` 副本，可再复制到 `%USERPROFILE%\.agent\skills\learning-notes`；该副本是否被自动发现取决于客户端配置。不要把备份目录存在等同于 Skill 已加载。

在支持 Skill 的客户端中调用：

> 使用 $learning-notes 把这些材料整理成学习笔记，讲清原理、因果、例子和适用边界，并关联已有知识。

仅制定规范时可以这样说：

> 使用 $learning-notes，为思源建立笔记分工、标签、双链和工具使用指导，不修改现有笔记。

写入思源需要另外配置可用的思源 MCP。本仓库不安装 MCP、不保存凭据。使用前按当前工具帮助确认实际能力；官方 MCP 的源码能力与当前部署的可用能力分别判断。

## 在思源中使用

将 `AGENTS.md` 保存为可见指导笔记，将 `SKILL.md` 正文与所需参考文件保存为关联页面。复制时把仓库相对链接替换为已创建页面的真实块引用，保留可读锚文本；不要粘贴不存在的块 ID。

普通指导笔记不会让所有 AI 会话自动加载规则。应在客户端项目指导或 MCP 工作区入口中明确要求读取它；只有获得维护入口的授权时才修改入口文件。

知识组织的重点是明确职责：文档树负责归属，导航负责阅读顺序，标签提供跨分区检索，真实块引用表达知识关系，反链和关系图用于发现关联。Mermaid 讲解图不会自动建立笔记之间的关系。

数据库、嵌入、模板、闪卡、资产和历史只在具体阅读或维护需求出现时使用；每项能力都有对应的使用与验证规则，详见工具规范。

## 设计来源

参考费曼式解释、Diátaxis、Obsidian 的知识关联方法，以及 [AI_Animation](https://github.com/Unclecheng-li/AI_Animation) 的内容层次与视觉组织。针对思源重新编写规范，不捆绑上游代码和模板。完整来源与具体取舍见[来源说明](skills/learning-notes/references/sources.md)。
