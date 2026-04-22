# BusCap Thermal Modeling Skill

## PR 风格说明

这次交付把 BusCap 相关流程整理成一个可复用的共享 skill，目标是让其他人直接通过 Copilot 复用当前仓库里已经稳定的 Python -> MATLAB -> Simulink 工作流，而不是重新摸索入口脚本。

本次上传范围刻意保持最小，只包含 skill 目录本身，不包含 `docs/`、`matlab/`、`artifacts/` 或数据文件。

## 本次新增目录

```text
.github/skills/buscap-thermal-modeling/
  SKILL.md
  references/
    architecture-and-principles.md
    copilot-prompt-examples.md
    outputs-and-artifacts.md
    plotting-and-reporting.md
    quick-start.md
    troubleshooting.md
    workflow-details.md
```

## 文件说明

### 1. SKILL.md

主入口文件，定义这个 skill 什么时候应该被命中、默认前提、最短操作路径、推荐执行顺序，以及怎样向 Copilot 提问更容易命中这个 skill。

### 2. references/quick-start.md

给第一次接触 BusCap 流程的同事使用，聚焦最短路径：更新参数、单文件对比、batch 对比、参数导出。

### 3. references/workflow-details.md

按阶段解释完整主流程，从 Python 导出参数到 MATLAB 参数脚本生成，再到 DAT 准备、单文件验证、Simulink 仿真和 batch 汇总。

### 4. references/outputs-and-artifacts.md

说明不同阶段会产出什么文件，便于别人快速判断流程是否跑成功，以及应该去哪里找结果。

### 5. references/troubleshooting.md

给常见问题排错用，重点覆盖：MATLAB 误差大、Simulink 偏差大、batch 跑不通、参数疑似过期、参数汇总失败。

### 6. references/architecture-and-principles.md

解释这个 skill 背后的最小原理：当前主线是 3NN，MATLAB 和 Simulink 共同复用 `buscap_model_step` 作为计算核心。

### 7. references/plotting-and-reporting.md

给 batch 结果做总览图时使用，说明输入文件、常用命令和三个典型输出图的解读方式。

### 8. references/copilot-prompt-examples.md

专门给最终使用者准备的提问模板和示例，已经按“新同事 / 回归验证 / 批量评估 / 排错”分组，方便直接复制给 Copilot。

## 适合分享给别人的一句话

这个 skill 把 BusCap 当前已经验证过的 Python -> MATLAB -> Simulink 流程打包成了一个可直接复用的 Copilot 入口，覆盖参数脚本生成、单文件验证、batch 对比、参数导出和绘图。

## 推荐阅读顺序

1. 先看 `.github/skills/buscap-thermal-modeling/SKILL.md`
2. 再看 `.github/skills/buscap-thermal-modeling/references/quick-start.md`
3. 如果要直接提问给 Copilot，用 `.github/skills/buscap-thermal-modeling/references/copilot-prompt-examples.md`
4. 如果要解释原理或排错，再看其他 references
