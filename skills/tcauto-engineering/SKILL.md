---
name: tcauto-engineering
description: 按明确要求读取 TCAUTO 保存的跨项目工程习惯原文，用于当前工程任务。
---

# TCAUTO 工程习惯

仅用户明确要求使用本入口，或项目 AGENTS.md/CLAUDE.md 明确要求时启用。仅启用 tcauto 不自动加载本入口。

读取 [跨项目工程习惯](references/跨项目工程习惯.md)，按当前任务需要采用。原文按字节保留，历史默认委派、ARIS 流程及多轮审查要求不执行：主 Agent 直接工作，仅用户要求时可选一个审阅 Agent。用户最新要求优先。

## Python 环境补充约定

本节为当前约定，原文中的环境管理要求按本节落实；本入口可独立使用，无需加载 tcauto。

- 所有项目的 Python 运行、脚本、依赖安装、测试和定时任务统一使用 Anaconda 管理的环境。先核实 Anaconda 安装位置，复用项目已确认的环境；需要新环境时按项目依赖创建，不默认使用 base。
- 执行前核对 `sys.executable`、`sys.prefix` 和 Python 版本。使用已核实的环境 Python 绝对路径，或 Anaconda 的 `conda run -p <环境绝对路径> ...`；不能依赖提示符或裸 `python`、`python3`、`pip` 判断环境。需用 pip 时，使用该环境的 `python -m pip`。不使用系统 Python、独立 venv、virtualenv 或 uv 管理的 Python 环境。
- 在目标项目实际使用的 `AGENTS.md`（或已有的 `Agents.md`）、`CLAUDE.md`（或已有的 `claude.md`）等项目入口记录环境；缺少这两个入口时补建，已有入口沿用原文件名。写明 Anaconda/conda 路径、环境名及绝对路径、Python 解释器及版本、依赖声明文件、创建或恢复命令、运行和测试命令。机器相关路径标注适用主机，迁移后重新核实；环境变化时同步更新各入口，避免相互冲突。
- Python 项目维护可复现的 `environment.yml` 或等效 Conda 环境声明，并在入口引用实际依赖文件。调度、子进程和可选审阅沿用已记录的环境。未找到可用 Anaconda 环境时说明缺失项，先完成不依赖 Python 的工作，不静默回退到其他解释器；安装环境仍遵循宿主权限要求。

需要定时续接时使用 tcauto；不自动建立调度、交接模板或项目长期启用指令。
