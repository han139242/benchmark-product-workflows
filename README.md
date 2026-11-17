# 项目调研与产品对标

一个可独立使用的 Codex Skill。适合做新项目、比较重要方案，或改善现有产品的关键流程。先多找一些真正不同的做法，再查有价值的候选，最后用自己的项目验证哪些做法值得借鉴。

## 调研结束会交付什么

1. 一组不同的候选做法，以及哪些条件筛掉了哪些候选。
2. 能点回原文的证据表，注明适用场景、版本和当前项目能否复现。
3. 用同一角色完成同一任务的对照结果，写清推荐做法、取舍和验收标准。

例如想改善工单列表，就让每个候选走完“筛选 → 打开详情 → 返回列表 → 恢复工作”这一条路径。记录各步结果和失败后的恢复方式，再决定哪些做法值得采用。从[对标工作表](references/benchmark-and-acceptance.md)开始。

## 安装

在 PowerShell 运行下面的命令。已有安装时沿用原目录。

```powershell
$codexRoot = if ($env:CODEX_HOME) { $env:CODEX_HOME } else { Join-Path $HOME '.codex' }
$legacy = Join-Path $codexRoot 'skills/benchmark-product-workflows'
$destination = Join-Path $HOME '.agents/skills/benchmark-product-workflows'
if ((Test-Path -LiteralPath $legacy) -or (Test-Path -LiteralPath $destination)) {
    throw 'Skill already installed. Use your existing copy.'
}
git clone https://github.com/han139242/benchmark-product-workflows.git $destination
```

如果用 Git 安装，在 Skill 目录运行 `git pull --ff-only` 即可更新。安装目录和发现方式见 [Codex Skills 文档](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills)。

## 单独使用

只装这个 Skill 就可以在 Codex 里做调研，无需配置 DSH、WorkBuddy 或 Python。给一次目标，说明想做什么决定，以及已有的约束。

> 用项目调研与产品对标 Skill，比较同类工单产品怎么保留列表筛选和未提交草稿。先多找一些不同做法，再核实最有价值的几种，给我原始链接、适用条件和推荐。先只调研。

也可以显式调用 `$benchmark-product-workflows`。Codex 会说明找了多少个不同候选、深查了哪些、各家哪项最适合你的任务，再把互补做法汇总成推荐方案，写清取舍和验证办法。需要实施时，在同一目标里写明改动范围和验收条件。流程和示例见 [Skill 说明](SKILL.md)与[工作表和验收示例](references/benchmark-and-acceptance.md)。

## 按 ISO/IEC 25010:2023 检查质量

整站、关键流程和重要方案可按[九项检查表](references/product-quality.md)查漏。优先核对功能完备性和交互能力，让同一个角色走完同一个任务，比较覆盖的分支、完成结果、状态反馈和失败恢复。外部产品的查证与本项目的实测分别留证。

## 与 Codex + 多模型协作配合使用

安装本 Skill，再按 [Codex + 多模型协作](https://github.com/han139242/codex-dsh-collaboration#安装)配置第二个 Skill。适合调研结论会影响重要取舍，或希望让其他模型找盲点的任务。用户可指定模型，也可让 Codex 从已有入口选；优先免费入口，新增费用由用户确认。

> 用项目调研与产品对标、Codex + 多模型协作，优化工单列表返回后筛选丢失的问题。先核实同类做法，交叉检查方案，再改动。验收时同一账号刷新后应保留筛选，切换账号时应使用各自的状态。

1. Codex 先查现状和同类项目。把会影响决定的发现摘到 `benchmark.md`，附一手链接、适用条件和本地验证方式。
2. 将同一目标、限制、验收标准和摘录交给独立模型核查。请它找遗漏角色、失败分支、适用边界或反例。Codex 查原始资料和实测核实后作最终决定。
3. 用户授权实施时，Codex 按原标准验证改动，重要改动可请模型带着本机实测结果复查。使用 DSH 路线时，细节见[交接工作表](references/benchmark-and-acceptance.md#与其他模型交接)。

## 本地记录与许可

候选池、调研记录、审查回复和运行日志留在本地，建议放在仓库外。公开仓库提供 Skill、参考工作表和虚构示例。与其他模型协作时，只共享任务允许的摘录和证据。

反馈问题或补充案例时，请附可公开复现的任务、原始来源和验证方法。提交前核对 README 和 Skill 里的链接、样例和检查口径。

本项目使用 [MIT 许可证](LICENSE)。
