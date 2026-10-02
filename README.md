# TCAUTO

**A compact Agent Skills collection for cross-project engineering, long-running work, scheduled continuation, and multi-agent review.**

TCAUTO 将跨项目工程习惯与精简的持续工作机制放在一起。模型随主会话更新；子 Agent 的思考深度按任务独立选择。领域工作沿用已有技能，例如 Nature 技能。

## 技能

| 入口 | 用途 |
|---|---|
| [`tcauto-engineering`](skills/tcauto-engineering/SKILL.md) | 新项目与工程工作的默认入口，读取完整跨项目工程习惯 |
| [`tcauto`](skills/tcauto/SKILL.md) | 长任务持续推进、断点交接、定时续接及多 Agent 审查 |

创建子 Agent 时必须显式填写 `model` 为已核实的主会话当前模型完整标识，不留空或依赖默认继承；用户最新明确模型选择优先，主会话换模后重新核对，技能不固定型号。无法核实模型时先确认，不静默回退。思考深度独立选 `low / medium / high / xhigh`，不使用 `max / ultra`。调度负责唤醒与续接，产物更新后再做必要审查；达到完成、截止或暂停条件后收尾。

自动研究开始前必须设置并回读有效 `/goal`；用户要求更新任务时同步已有 goal，续接和阶段检查对照最新目标与完成条件。心跳负责唤醒，不能替代 goal；目标机制不可用或无法完成必要更新时先说明限制并解决，再进入自动研究。

## 原文

[`跨项目工程习惯.md`](skills/tcauto-engineering/references/跨项目工程习惯.md) 原样收录用户指定的《跨项目工程习惯(4).md》，不删节、不润色、不调整换行。文件为70,064字节，SHA-256：

```text
65f78a07875b7d034e5988bd99b9fc2b83524e22609a31f3b2f59932d4a971ba
```

## 安装与使用

把 `skills/` 下的 `tcauto` 与 `tcauto-engineering` 两个完整目录安装到代理的用户级技能目录。Codex 当前文档使用 `~/.agents/skills/`；仍使用 `~/.codex/skills/` 的环境按实际发现目录安装，避免同名重复安装。也可请 `$skill-installer` 从本仓库安装这两个目录。

要让每次新项目与工程工作默认遵循 TCAUTO，安装后还须在 Codex 的用户级 `~/.codex/AGENTS.md` 中加入以下入口；仅复制技能目录不等于设置默认工作约定：

```markdown
每次新建项目、开始或恢复工程工作，先使用 TCAUTO 的 tcauto-engineering，读取其中的跨项目工程习惯原文并按适用约定执行。长任务使用 tcauto 管理持续推进、定时续接与独立审查。自动研究开始前必须设置有效 goal；用户要求更新任务时同步已有 goal，续接对照最新目标，按当前目标工具条件执行。创建子 Agent 时必须显式填写 model 为已核实的主会话当前模型完整标识，不省略或依赖默认继承，用户最新明确模型选择优先。思考深度独立按任务从 low、medium、high、xhigh 选择，不使用 max、ultra。
```

调用示例：`$tcauto-engineering 开始当前工程工作`；`$tcauto 持续完成当前已授权任务`。

定时任务依赖宿主和代理提供的调度能力；机器休眠或应用关闭时不保证继续运行。技能不扩大项目权限或资源授权。

配置依据：[Codex 技能](https://learn.chatgpt.com/docs/build-skills)、[全局与项目 AGENTS.md](https://learn.chatgpt.com/docs/agent-configuration/agents-md)。

## 许可证

MIT，见 [LICENSE](LICENSE)。
