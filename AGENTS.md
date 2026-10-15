# TCAUTO 仓库维护

维护本仓库时使用 skills/tcauto/SKILL.md。主 Agent 直接修改；仅用户要求时可选一个审阅 Agent，不进行多 Agent 协同。

工程习惯原文按字节保留，不执行其中历史 ARIS 或默认多 Agent 流程。修改工程习惯入口时才读取 skills/tcauto-engineering/SKILL.md。只发布技能集文件。

## Python 环境

所有项目的 Python 执行、依赖安装、测试、子进程和定时任务必须使用 Anaconda 管理的环境。按 [tcauto 的 Python 环境流程](skills/tcauto/SKILL.md#python-环境)核实环境，并把实际环境和命令同步记录到目标项目的 AGENTS.md、CLAUDE.md 等入口；沿用已有文件名大小写。不使用系统 Python、独立 venv、virtualenv 或 uv 管理的 Python 环境，不静默回退。

本仓库只有技能集，无 Python 应用、运行依赖或项目测试套件，不需要创建业务环境或 environment.yml。以下为本次维护已核实的技能校验环境，仅适用于 tchuian 当前 macOS 主机，其他主机需重新核实：

| 项目 | 实际值 |
|---|---|
| Anaconda 根目录 / 环境路径 | `/Volumes/新加卷/anaconda3` |
| conda 路径及版本 | `/Volumes/新加卷/anaconda3/bin/conda`，26.5.3 |
| 环境名 | `base`，仅复用现有环境进行技能校验 |
| Python 解释器及版本 | `/Volumes/新加卷/anaconda3/bin/python`，3.14.6 |
| 校验依赖 | PyYAML 6.0.3；仓库无依赖声明文件 |
| 创建或恢复 | 复用已安装的 Anaconda base；如需独立校验环境，使用已核实的 Anaconda conda 执行 `conda create -n tcauto-validation python=3.14 pyyaml=6.0.3`，再核实并更新入口中的路径和版本 |

在仓库根目录执行（校验器属于宿主 skill-creator，其他主机需定位其实际位置）：

```sh
'/Volumes/新加卷/anaconda3/bin/python' -c 'import sys; print(sys.executable); print(sys.prefix); print(sys.version)'
'/Volumes/新加卷/anaconda3/bin/python' /Users/tchuian/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/tcauto
'/Volumes/新加卷/anaconda3/bin/python' /Users/tchuian/.codex/skills/.system/skill-creator/scripts/quick_validate.py skills/tcauto-engineering
git diff --check
shasum -a 256 skills/tcauto-engineering/references/跨项目工程习惯.md
```

环境变化时同步更新本文件和 CLAUDE.md；不要把本机绝对路径作为其他项目的默认路径。
