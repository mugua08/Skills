# BusCap Thermal Modeling Skill Overview

## What This Is

This document is the English root-level sharing note for the BusCap thermal modeling skill.

The skill packages an already-validated workflow for Python -> MATLAB -> Simulink collaboration, so teammates can reuse the current execution path instead of rediscovering scripts, commands, and ordering on their own.

## What It Covers

The skill supports these common tasks:

- converting Python-exported `thermal_model_export.mat` into MATLAB parameter script form
- generating `buscap_nn_params.m`
- validating a single DAT file with MATLAB replay
- running single-file MATLAB / Simulink comparison
- running batch comparison on `INCA_Data`
- exporting current Simulink runtime parameters
- generating batch overview plots from `per_file_metrics.csv`

## Main Entry Points

- `.github/skills/buscap-thermal-modeling/SKILL.md`
- `.github/skills/buscap-thermal-modeling/references/quick-start.md`
- `.github/skills/buscap-thermal-modeling/references/copilot-prompt-examples.md`

## Related Root Documents

- `BUSCAP_THERMAL_MODELING_PR_SUMMARY.md`
- `BUSCAP_THERMAL_MODELING_SHARE_BLURB.md`
- `SKILLS_INDEX.md`

## Why This Skill Exists

The point of this skill is not to create another abstraction layer. The point is to make the existing stable workflow discoverable, reusable, and easier to invoke through Copilot.

## Recommended Reading Order

1. Read `.github/skills/buscap-thermal-modeling/SKILL.md`
2. Follow `.github/skills/buscap-thermal-modeling/references/quick-start.md`
3. Use `.github/skills/buscap-thermal-modeling/references/copilot-prompt-examples.md` when prompting Copilot
4. Read `BUSCAP_THERMAL_MODELING_PR_SUMMARY.md` if you want the file-by-file breakdown
5. Use `BUSCAP_THERMAL_MODELING_SHARE_BLURB.md` if you want a ready-to-send bilingual mail/IM template

## One-Sentence Summary

This skill turns the current BusCap Python -> MATLAB -> Simulink workflow into a reusable Copilot entry for parameter generation, validation, batch comparison, parameter export, and reporting.
