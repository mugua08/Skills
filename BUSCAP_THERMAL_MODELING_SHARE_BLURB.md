# BusCap Thermal Modeling Share Template

## 用途

这份文档把中文短版和英文短版统一成一套可以直接复制到邮件、IM、群消息里的双语模板。

## 中文 IM 短版

BusCap 这套共享 skill 已经把当前验证过的 Python -> MATLAB -> Simulink 流程整理成可直接复用的 Copilot 入口，覆盖参数脚本生成、单文件验证、batch 对比、参数导出和批量绘图。入口在 `.github/skills/buscap-thermal-modeling/SKILL.md`，第一次使用建议先看 `references/quick-start.md`，如果想直接提问给 Copilot，可以参考 `references/copilot-prompt-examples.md`。

## 中文邮件短版

大家好，

我把 BusCap 当前已经验证过的 Python -> MATLAB -> Simulink 流程整理成了一个共享 Copilot skill，目标是让后续同事可以直接复用参数生成、单文件验证、batch 对比、参数导出和绘图流程，而不是再单独摸索脚本入口。

建议从以下文件开始：

- `.github/skills/buscap-thermal-modeling/SKILL.md`
- `.github/skills/buscap-thermal-modeling/references/quick-start.md`
- `.github/skills/buscap-thermal-modeling/references/copilot-prompt-examples.md`

如果只是想快速理解这次交付包含什么，可以再看根目录的 `BUSCAP_THERMAL_MODELING_PR_SUMMARY.md`。

## English IM Short Version

The BusCap shared skill now packages the validated Python -> MATLAB -> Simulink workflow into a reusable Copilot entry. It covers parameter script generation, single-file validation, batch comparison, parameter export, and batch plotting. Start with `.github/skills/buscap-thermal-modeling/SKILL.md`, then use `references/quick-start.md` and `references/copilot-prompt-examples.md` for actual usage.

## English Email Short Version

Hi all,

I packaged the current validated BusCap Python -> MATLAB -> Simulink workflow into a shared Copilot skill so teammates can reuse the existing path instead of rediscovering scripts and execution order.

The skill covers:

- parameter script generation
- single-file validation
- batch comparison
- parameter export
- reporting plots

Recommended starting points:

- `.github/skills/buscap-thermal-modeling/SKILL.md`
- `.github/skills/buscap-thermal-modeling/references/quick-start.md`
- `.github/skills/buscap-thermal-modeling/references/copilot-prompt-examples.md`

If you want the file-by-file summary of what was added, see `BUSCAP_THERMAL_MODELING_PR_SUMMARY.md`.
