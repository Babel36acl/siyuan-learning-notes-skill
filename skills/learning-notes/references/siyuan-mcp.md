# 思源 MCP 的能力与实际使用

## 先判断当前环境

这是工具路由参考，不是固定工具清单。开始思源任务时确认本轮可调用工具，读取当前用户规则和工作区入口；Sisyphus 使用 `fs(action="read", path="/USER_RULES.md")` 与 `/AGENTS.md`。旧记忆与当前用户要求冲突时采用当前要求，不把旧的强制证据链带回学习笔记。

需要非平凡操作时读 `siyuan://skills/index`，再选最窄的场景 Skill。操作参数查当前 action help；资源读取不可用可使用工具的 `action="help"`。不要加载全部帮助。

先对可用连接进行只读检查，并记录工具发现结果。连接初始化失败时，不声称其读写测试通过；恢复后重新发现工具并验证。不把 Sisyphus 的 action 参数直接发给官方入口，不在 Skill 或笔记中保存认证头、Token 或凭据。

## 官方 MCP：以源码为候选，按当前端点确认

检查官方仓库提交 `8641553a1f07374001902d3ce773285db1292b2d` 的 `kernel/mcp/tools` 得到以下能力。它们是候选路由，须等当前连接实际暴露相同 schema 后再使用。

| 官方源码工具 | 适合学习笔记的能力 |
| --- | --- |
| `document`、`block` | 创建/查询文档，读取和编辑 Markdown、Kramdown、DOM 及子块 |
| `search`、`ref`、`outline` | 全文与语义搜索、附件全文、反链/提及、标题树；语义搜索依赖 embedding 配置 |
| `attr` | 块属性、图标、标题图等；接口不同于 Sisyphus 的 document.set_attr |
| `database` | 数据库字段和条目，table/gallery/kanban 布局及关系字段 |
| `asset` | 附件，以及 `create_html` 创建 HTML 资产并插入沙箱 IFrame |
| `template`、`skill` | 模板与服务端 Skill 的管理；保存 Skill 不等于写一篇指导笔记 |

`asset.create_html` 的源码限制是最多 2 MiB HTML，生成 `sandbox="allow-scripts"` IFrame；可用于可选的交互解释，不能仅凭它存在就声称用户当前环境可以运行。`asset.upload` 读取思源服务端可访问的文件路径，远程 MCP 不能当然读取 Codex 本机文件。不要混用两个服务器的参数与路径。

## Sisyphus：按任务选择

| 任务 | 已暴露的工具与操作 | 容易混淆的边界 |
| --- | --- | --- |
| 浏览、读普通正文、创建页面 | `fs.ls/read/search/write/replace` | path 包含笔记本名；不是磁盘路径 |
| 定位和元数据 | `document.lookup/get_doc/get_outline/set_attr` | lookup 的 path 是存储路径，hpath 是笔记本内人类路径 |
| 原生块和精确修改 | `block.get_kramdown/get_children/append/insert/update/set_attrs` | update 通常替换一个块，多个兄弟块用 append/insert |
| 全文、相关知识和反链 | `search.fulltext/semantic/get_backlinks/search_refs` | 语义结果需核对正文，不能当同义概念证明 |
| 必要的结构查询 | `search.query_sql` | 仅 SELECT，显式 LIMIT，遵守笔记本读取权限 |
| 属性视图数据库 | `av.get/render/add_rows/set_cells` 等 | Markdown 表格或 AV 占位 HTML 不等于真实数据库 |
| 附件与导出 | `file` 对应帮助 | 图片内容需实际读取，已有 OCR 不等于重新识别 |
| 复习 | `flashcard.create_card/get_decks/list_cards` 等 | 绑定元数据不等于完成闪卡注册 |
| 历史 | `timeline` 对应帮助 | 需要时才建快照；回滚不是普通编辑 |

上表来自编写时实际发现的接口，并非每个部署都具备全部能力。数据库、附件或闪卡需在实际使用时验证，不把工具存在等同功能已经测试通过。

## 笔记写入流程

1. 搜索同主题页并读取目标。普通文档用 `/笔记本/文件夹/标题`；选择已有合适笔记本，避免制造平行知识库。
2. 新建普通页面用 `fs.write`，正文不重复写首个 H1，因为文档标题自动显示。已有页面只做本次范围内的修改；整页覆盖需先确认不是复杂原生块容器。
3. Sisyphus 启用 strict safe writes 时：同一精确操作先传 `validateOnly=true`，再按返回要求执行。若新建文档预检仅返回 `requestIdRequired`，则执行时使用新 UUIDv7 `requestId`；属性修改和虚拟文件替换若返回 `preconditionField`、短 hash 与租约，须将对应凭据传回。不能假造未返回的 hash 或复用过期租约。内容变化或租约过期时只对新请求重新预检。请求结果不确定时先读回，不盲目重复新建。
4. 创建后使用 `document.set_attr` 的 `attrs.icon` 设置图标，参数格式以实际帮助和读回为准。图标沿用用户工作区的语义习惯。
5. 回读正文、图标；实际用了块引用则检查目标和反链，用了原生布局则查看块树。仅做实际内容需要的验证，不测试无关功能。

权限拒绝与连接故障分开处理：前者不能换接口绕过，后者可以继续使用已授权且正常的 MCP。传输成功但结果 `isError` 或业务失败仍是失败；不得写成完成。

## 原生内容不应被压平

普通正文可用 fs；已有超级块、数据库、媒体、查询嵌入、挂件或精确块引用关系时用 document/block/av 按块修改。Markdown 整篇重写可能改变块 ID 或丢失结构，不能把 AV 占位符当数据本身。

真正双链的形态为 `((真实块ID '可读锚文本'))`。先查询目标再构造引用；`[标题](siyuan://blocks/真实ID)` 是可打开链接，不产生同样的反链语义。思源标签是 `#主题#`，书签是块属性。不要为凑链接数量创建空页面。

`/AGENTS.md` 是 Sisyphus 虚拟工作区指导文件，不等于用户能在文档树看到的普通笔记。用户要求 AI 指导笔记时创建可见页面；只有获准维护工作区指导时才更新虚拟文件中的有关条款，并保留原件和无关内容。新增一篇 AGENTS.md 普通笔记不代表所有 MCP 或新会话都会自动读取它；需要明确入口或调用约定。
