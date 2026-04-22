# Skills

A small repository for reusable Copilot skills and sharing notes.

## Featured Skill

### BusCap Thermal Modeling

This skill packages an already-validated BusCap workflow for Python -> MATLAB -> Simulink collaboration. It is designed for teams that need a reusable entry point instead of rediscovering scripts and execution order every time.

It covers:

- exporting Python model parameters into MATLAB parameter script format
- generating `buscap_nn_params.m`
- running single-file MATLAB replay and MATLAB / Simulink comparison
- running batch comparison on DAT files
- exporting current Simulink runtime parameters
- generating batch overview plots from `per_file_metrics.csv`

## Quick Links

- Skill entry: `.github/skills/buscap-thermal-modeling/SKILL.md`
- Quick start: `.github/skills/buscap-thermal-modeling/references/quick-start.md`
- Prompt examples: `.github/skills/buscap-thermal-modeling/references/copilot-prompt-examples.md`
- PR-style overview: `BUSCAP_THERMAL_MODELING_PR_SUMMARY.md`
- Share blurb: `BUSCAP_THERMAL_MODELING_SHARE_BLURB.md`
- English overview: `BUSCAP_THERMAL_MODELING_OVERVIEW_EN.md`

## When To Use This Skill

Use it when you want Copilot to help with one of these tasks:

- connect `thermal_model_export.mat` to the MATLAB / Simulink workflow
- validate one DAT file with MATLAB or MATLAB / Simulink comparison
- run a full batch comparison on `INCA_Data`
- export parameter summary files for review
- generate reporting plots from batch metrics

## Recommended Starting Point

1. Open `.github/skills/buscap-thermal-modeling/SKILL.md`
2. Follow `.github/skills/buscap-thermal-modeling/references/quick-start.md`
3. Reuse `.github/skills/buscap-thermal-modeling/references/copilot-prompt-examples.md` when prompting Copilot

## Why This Repo Entry Matters

The goal is not to invent a new wrapper around the workflow. The goal is to expose the current stable workflow in a format that other people can discover, invoke, and reuse quickly.
