# TCAUTO 仓库维护

遵循 AGENTS.md；主 Agent 直接工作，仅用户要求时可选一个审阅 Agent。其他项目仅在用户或项目明确要求时启用 TCAUTO。

## Python 环境

所有项目的 Python 执行、依赖安装、测试、子进程和定时任务必须使用 Anaconda 管理的环境。不使用系统 Python、独立 venv、virtualenv 或 uv 管理的 Python 环境，不静默回退。目标项目的 AGENTS.md、CLAUDE.md 等入口必须同步记录已核实的环境与运行命令，沿用已有文件名大小写。

本仓库仅含技能集，没有 Python 应用或项目依赖声明。当前 macOS 主机（tchuian）技能校验复用 Anaconda `base`：

- Anaconda / 环境绝对路径：`/Volumes/新加卷/anaconda3`。
- conda：`/Volumes/新加卷/anaconda3/bin/conda`，26.5.3。
- Python：`/Volumes/新加卷/anaconda3/bin/python`，3.14.6；校验依赖 PyYAML 6.0.3。
- 创建或恢复方式、完整校验命令见 [AGENTS.md 的 Python 环境](AGENTS.md#python-环境)。没有业务运行命令；技能通过宿主加载。

执行前核对 `sys.executable`、`sys.prefix` 和版本。跨主机或环境变化时重新核实并同步更新两个入口，不照搬本机路径。
