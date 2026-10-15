# TCAUTO

轻量技能集：主 Agent 直接完成任务，保留定时续接和可选的一个审阅 Agent。

仅用户明确要求使用，或项目 AGENTS.md/CLAUDE.md 明确要求时启用。默认不创建子 Agent；不因任务复杂自动协同，不包含 ARIS 管理流程、多角色分工、多轮审查或固定交接模板。

| 技能 | 用途 |
|---|---|
| [tcauto](skills/tcauto/SKILL.md) | 定时续接，可选单个审阅 Agent |
| [tcauto-engineering](skills/tcauto-engineering/SKILL.md) | 按明确要求读取跨项目工程习惯原文 |

两个入口独立使用。tcauto 不自动加载工程习惯全文。审阅 Agent 仅在用户要求时启用，显式指定主会话当前模型，深度独立选 low、medium、high、xhigh。

定时任务使用宿主正式调度工具，完成、截止或暂停后停止。自动研究设置有效 goal，用户调整目标时同步；不附加其他管理流程。

## Python 环境流程

两个技能入口均要求：所有项目的 Python 运行、依赖安装、测试和定时任务使用 **Anaconda 管理的环境**。

1. 核实当前主机的 Anaconda 安装及项目环境，复用已确认的项目环境；需要新环境时按项目依赖创建。
2. 核对 `sys.executable`、`sys.prefix` 和 Python 版本，用环境 Python 绝对路径或 Anaconda 的 `conda run -p <环境绝对路径> ...` 执行；pip 使用该环境的 `python -m pip`。
3. 将 conda 路径、环境名和绝对路径、解释器及版本、依赖声明、创建或恢复命令、运行和测试命令写入项目 `AGENTS.md`、`CLAUDE.md` 等入口。沿用已有 `Agents.md`、`claude.md` 等文件名；缺少入口时补建，环境变化时同步更新。
4. Python 项目维护 `environment.yml` 或等效 Conda 环境声明。定时续接及子进程沿用入口记录的环境；未找到可用环境时明确说明，不回退到系统 Python、独立 venv、virtualenv 或 uv 管理的 Python 环境。

本仓库没有 Python 应用，仅在维护时使用 Python 校验技能；本机已核实的校验环境及命令见 [AGENTS.md](AGENTS.md#python-环境) 和 [CLAUDE.md](CLAUDE.md#python-环境)。这些主机路径不作为其他项目的默认配置。

## 安装

将 skills 下的两个完整目录放入宿主实际使用的技能目录。两个入口均关闭隐式调用；安装本身不会启用，单次调用不会永久启用项目。

## 工程习惯原文

[跨项目工程习惯.md](skills/tcauto-engineering/references/跨项目工程习惯.md) 原样保存用户指定的《跨项目工程习惯(4).md》，70,064字节。历史 ARIS、默认委派和多轮审查要求不执行，当前用户要求优先。

SHA-256：`65f78a07875b7d034e5988bd99b9fc2b83524e22609a31f3b2f59932d4a971ba`

## 许可证

[MIT](LICENSE)。
