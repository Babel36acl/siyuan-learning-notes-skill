# 来源与取舍

此页服务 Skill 维护，普通学习笔记不携带这份来源清单。提炼日期：2026-09-10。

| 实际检查的来源 | 吸收 | 不迁移 |
| --- | --- | --- |
| `feynman-technique/SKILL.md` | 因果解释、最小例子、理解缺口、预测题、按共同机制综合 | 全会话采集、固定 Evidence/Guardrail 栏目 |
| `index-note/SKILL.md` | 少量入口、说明阅读价值与顺序 | 全量分类树、机械修改所有反链 |
| `note-split/SKILL.md` | 按独立问题拆分、前提/应用/反例关联 | 强制篇数、强制链接配额 |
| `obsidian-markdown/SKILL.md` | 清楚层次、可读链接、公式与提示 | 未适配的 wikilink、块 ID、主题语法 |
| `obsidian-bases/SKILL.md` | 少量元数据和不同阅读入口 | `.base` 或 YAML 查询冒充思源数据库 |
| `research/SKILL.md` | 需要研究时优先一手资料 | 每项主张强制引用、固定后台代理、固定 repo 输出 |
| [make-note](https://github.com/birbirbrian/make-note-skills/blob/main/skills/make-note/SKILL.md) | 从对话提炼学习目标与关键问题，把问题放在相关解释旁 | 作者私有模板路径、强制繁体中文/无空格标题/Recall、允许不存在的双链 |
| [docs-writing](https://github.com/mblode/agent-skills/blob/main/skills/docs-writing/SKILL.md) 与 [Diátaxis Explanation](https://diataxis.fr/explanation/) | 按阅读任务区分解释/教程/操作/参考，解释概念之间的联系与背景 | 全套文档审计、每篇强制执行示例和输出命令日志 |
| [human-readable-reports](https://github.com/SummerRiversound/human-readable-reports/blob/main/SKILL.md) | 完整因果句、自然语言表格、术语解释、简短末注 | 强制比喻、未验证的 HTML details 折叠 |
| [technical-writing](https://github.com/luoling8192/technical-writing/blob/main/SKILL.md) | 平实中文、删无信息过场句、把空评价改成具体条件和结果、统一术语 | 评审/汇报模板与证据优先叙事 |
| [codex-knowledge-base-skill / project-knowledge-maintainer](https://github.com/chancy24/codex-knowledge-base-skill/blob/main/skills/project-knowledge-maintainer/SKILL.md) | 更新既有知识、协调重复/过时/矛盾、区分事实与推测 | 固定七文档、强制 changelog、未来 Agent 接手导向 |
| [AI_Animation / scholar-notes](https://github.com/Unclecheng-li/AI_Animation/tree/master/skills/scholar-notes) | 标题层次、语义强调、过程图、对比和旁注 | 固定纸高、压缩正文、强制字体/图标库/动画 |
| Sisyphus `siyuan://help/ai-layout-guide`、`skill://siyuan-mcp-write-format/SKILL.md`、实际 action help | 原生结构、路径语义、按块操作、严格写入与读回 | 全能力强制启用、把工具宣称当端到端验证 |
| [思源原生格式](https://github.com/siyuan-note/siyuan/blob/master/docs/SY-FORMAT.md)、[Kernel API](https://github.com/siyuan-note/siyuan/blob/master/docs/API.md) | 验证块引用、超级块、媒体结构和块 API | 把 Kernel API 直接等同 MCP 暴露接口 |
| [官方 MCP 源码](https://github.com/siyuan-note/siyuan/tree/8641553a1f07374001902d3ce773285db1292b2d/kernel/mcp/tools) | 官方 document/block/ref/asset/database 等实际 schema；HTML 沙箱与服务端路径限制 | 将 master 源码能力宣称为用户在线端点已通过测试 |
| 用户指定的 [思源用户指南入口](https://siyuannote.com/article/1724525755) 及其标签、关系图、块引用、Markdown 输入页 | 理解各界面工具职责、层级标签和静态/动态锚文本 | 非官方教程不替代当前 MCP 参数；界面输入快捷方式不等于 API 持久语法 |

AI_Animation 检查版本为 `cc448d43b75d4b53c2e785240777b09823d22a68`，读取 scholar-notes 的 Skill、布局和组件参考，仅提炼方法。上述本地 Skill 名称表示实际检查过的材料，不表示本仓库分发它们；有公开原始仓库的来源已附链接。

make-note、docs-writing、human-readable-reports、technical-writing 与 codex-knowledge-base-skill 的核心文件已从上述原始仓库获取并分析。本仓库提供重新编写的整合规范，不捆绑上游代码、模板或依赖。
