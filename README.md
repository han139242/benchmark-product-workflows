# 项目调研与产品对标

一个可独立使用的 Codex Skill。适合做新项目、比较重要方案，或改善现有产品的关键流程。先多找一些真正不同的做法，再查有价值的候选，最后用自己的项目验证哪些做法值得借鉴。

## 安装

在 PowerShell 运行下面的命令。已安装同名 Skill 时，沿用现有安装。

```powershell
$skillsDir = Join-Path $HOME '.agents/skills'
$destination = Join-Path $skillsDir 'benchmark-product-workflows'
git clone https://github.com/han139242/benchmark-product-workflows.git $destination
```

如果用 Git 安装，在 Skill 目录运行 `git pull --ff-only` 即可更新。安装目录和发现方式见 [Codex Skills 文档](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills)。

## 单独使用

只装这个 Skill 就可以在 Codex 里做调研，无需配置 DSH、WorkBuddy 或 Python。给一次目标，说明想做什么决定，以及已有的约束。

> 用项目调研与产品对标 Skill，比较同类工单产品怎么保留列表筛选和未提交草稿。先多找一些不同做法，再核实最有价值的几种，给我原始链接、适用条件和推荐。先只调研。

也可以显式调用 `$benchmark-product-workflows`。Codex 会说明实际找了多少个候选、核实了哪些做法，并给出采用、暂缓或继续验证的理由。需要实施时，在同一目标里写明改动范围和验收条件。完整流程和可填写的对照项见 [Skill 说明](SKILL.md)与[工作表和验收示例](references/benchmark-and-acceptance.md)。

## 与 Codex + DSH 配合使用

安装本 Skill，再按 [Codex + DSH 协作](https://github.com/han139242/codex-dsh-collaboration#安装)配置第二个 Skill。适合调研结论会影响重要取舍，或希望另一模型找盲点的任务。

> 用项目调研与产品对标、Codex + DSH 协作，优化工单列表返回后筛选丢失的问题。先核实同类做法，交叉检查方案，再改动。验收时同一账号刷新后应保留筛选，切换账号时应使用各自的状态。

1. Codex 先查现状和同类项目。共享目标、限制和验收标准写入 `goal.txt`。把会影响决定的发现摘到 `benchmark.md`，附一手链接、适用条件和本地验证方式。
2. 协作 Skill 通过 `--benchmark` 把摘录和同一目标交给 DSH。DSH 可以提不同方案、适用边界或遗漏的验收项。Codex 回到原始资料和本机实测核实，由 Codex 最终决定。
3. 用户授权实施时，Codex 按原标准验证改动。关键改动需要复查时，通过 `--evidence` 传递相关实测结果。

## 本地记录与许可

候选池、调研记录、审查回复和运行日志留在本地，建议放在仓库外。公开仓库提供 Skill、参考工作表和虚构示例。与 DSH 协作时，只共享任务允许的摘录和证据。

本项目使用 [MIT 许可证](LICENSE)。
