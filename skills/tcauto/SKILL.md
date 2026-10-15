---
name: tcauto
description: 按明确要求启用 TCAUTO，单 Agent 工作，支持定时续接和可选的一个审阅 Agent。
---

# TCAUTO

仅用户明确要求使用 TCAUTO，或项目 AGENTS.md/CLAUDE.md 明确要求时启用。一次调用不自动永久启用项目。

主 Agent 直接完成任务，跑通后做必要测试。默认不创建子 Agent，不建立多角色协同、多轮审查、固定交接模板或额外验证门槛。不自动加载 tcauto-engineering 或工程习惯全文。

## Python 环境

- 所有项目的 Python 运行、脚本、依赖安装、测试和定时任务统一使用 Anaconda 管理的环境。先核实 Anaconda 安装位置，复用项目已确认的环境；需要新环境时按项目依赖创建，不默认使用 base。
- 执行前核对 `sys.executable`、`sys.prefix` 和 Python 版本。使用已核实的环境 Python 绝对路径，或 Anaconda 的 `conda run -p <环境绝对路径> ...`；不能依赖提示符或裸 `python`、`python3`、`pip` 判断环境。需用 pip 时，使用该环境的 `python -m pip`。不使用系统 Python、独立 venv、virtualenv 或 uv 管理的 Python 环境。
- 在目标项目实际使用的 `AGENTS.md`（或已有的 `Agents.md`）、`CLAUDE.md`（或已有的 `claude.md`）等项目入口记录环境；缺少这两个入口时补建，已有入口沿用原文件名。写明 Anaconda/conda 路径、环境名及绝对路径、Python 解释器及版本、依赖声明文件、创建或恢复命令、运行和测试命令。机器相关路径标注适用主机，迁移后重新核实；环境变化时同步更新各入口，避免相互冲突。
- Python 项目维护可复现的 `environment.yml` 或等效 Conda 环境声明，并在入口引用实际依赖文件。调度、子进程和可选审阅沿用已记录的环境。未找到可用 Anaconda 环境时说明缺失项，先完成不依赖 Python 的工作，不静默回退到其他解释器；安装环境仍遵循宿主权限要求。

## 可选审阅

用户要求审阅时，可创建一个审阅 Agent，检查已完成的产物并反馈具体问题；主 Agent 修复必要问题后交付。不委派实现、不派生其他 Agent、不循环审阅。
创建时显式指定已核实的主会话模型完整标识；用户最新模型选择优先，不固定型号。思考深度独立选 low、medium、high、xhigh，不使用 max、ultra。

## 定时续接

用户要求定时或持续工作时，使用宿主正式调度工具；Codex Desktop 使用 automation_update，优先复用当前会话 heartbeat。按用户要求设定时间，未指定周期时用30分钟。
提示仅记录目标、工作区、下一步、停止条件；涉及 Python 时同时指向项目入口中已核实的 Anaconda 环境和执行命令。续接已有进度，避免重复执行；无变化保持安静，有实质结果、失败或需要用户行动时通知。
调度支持模型参数时显式使用主会话模型。完成、截止或暂停时停止本任务调度，不自动恢复已暂停任务。调度不可用时说明限制。

自动研究开始前按工具授权条件设置有效 goal；用户调整目标时同步已有 goal。goal 与定时唤醒各司其职，不额外建立管理流程。
