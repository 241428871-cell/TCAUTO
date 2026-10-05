# TCAUTO

轻量技能集：主 Agent 直接完成任务，保留定时续接和可选的一个审阅 Agent。

仅用户明确要求使用，或项目 AGENTS.md/CLAUDE.md 明确要求时启用。默认不创建子 Agent；不因任务复杂自动协同，不包含 ARIS 管理流程、多角色分工、多轮审查或固定交接模板。

| 技能 | 用途 |
|---|---|
| [tcauto](skills/tcauto/SKILL.md) | 定时续接，可选单个审阅 Agent |
| [tcauto-engineering](skills/tcauto-engineering/SKILL.md) | 按明确要求读取跨项目工程习惯原文 |

两个入口独立使用。tcauto 不自动加载工程习惯全文。审阅 Agent 仅在用户要求时启用，显式指定主会话当前模型，深度独立选 low、medium、high、xhigh。

定时任务使用宿主正式调度工具，完成、截止或暂停后停止。自动研究设置有效 goal，用户调整目标时同步；不附加其他管理流程。

## 安装

将 skills 下的两个完整目录放入宿主实际使用的技能目录。两个入口均关闭隐式调用；安装本身不会启用，单次调用不会永久启用项目。

## 工程习惯原文

[跨项目工程习惯.md](skills/tcauto-engineering/references/跨项目工程习惯.md) 原样保存用户指定的《跨项目工程习惯(4).md》，70,064字节。历史 ARIS、默认委派和多轮审查要求不执行，当前用户要求优先。

SHA-256：`65f78a07875b7d034e5988bd99b9fc2b83524e22609a31f3b2f59932d4a971ba`

## 许可证

[MIT](LICENSE)。
