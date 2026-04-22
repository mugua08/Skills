# Skills

Reusable Copilot skills, lightweight guides, and sharing notes for engineering workflows.

## Why This Repository Exists

This repository is meant to collect skills that are practical, reusable, and easy for other people to discover. Each skill should help teammates invoke an existing workflow faster instead of rediscovering scripts, commands, and execution order from scratch.

## Featured Skill

### BusCap Thermal Modeling

A reusable Copilot skill for the current BusCap Python -> MATLAB -> Simulink workflow.

It is built for teams that need a stable entry point for:

- converting Python-exported model artifacts into MATLAB parameter script form
- generating `buscap_nn_params.m`
- validating a single DAT file in MATLAB
- running single-file MATLAB / Simulink comparison
- running batch comparison on `INCA_Data`
- exporting current Simulink runtime parameters
- generating reporting plots from `per_file_metrics.csv`

## Quick Start

1. Open `.github/skills/buscap-thermal-modeling/SKILL.md`
2. Read `.github/skills/buscap-thermal-modeling/references/quick-start.md`
3. Reuse `.github/skills/buscap-thermal-modeling/references/copilot-prompt-examples.md` when prompting Copilot

## Repository Navigation

- Skill entry: `.github/skills/buscap-thermal-modeling/SKILL.md`
- Quick start: `.github/skills/buscap-thermal-modeling/references/quick-start.md`
- Prompt examples: `.github/skills/buscap-thermal-modeling/references/copilot-prompt-examples.md`
- PR-style overview: `BUSCAP_THERMAL_MODELING_PR_SUMMARY.md`
- Bilingual mail/IM template: `BUSCAP_THERMAL_MODELING_SHARE_BLURB.md`
- English overview: `BUSCAP_THERMAL_MODELING_OVERVIEW_EN.md`
- Skill index: `SKILLS_INDEX.md`

## When To Use The BusCap Skill

Use this skill when you want Copilot to help with one of these tasks:

- connect `thermal_model_export.mat` to the MATLAB / Simulink workflow
- validate one DAT file with MATLAB replay
- run a full MATLAB / Simulink comparison on one file
- run a batch comparison across `INCA_Data`
- export parameter summary files for review
- generate batch plots for reporting

## Skill Design Principle

The goal is not to build a new wrapper around the workflow. The goal is to expose the current stable workflow in a format that is discoverable, reusable, and easier to share with other people.

## Current Skills

- BusCap Thermal Modeling: `.github/skills/buscap-thermal-modeling/`

## Next Skills

This repository is structured so more skills can be added later under `.github/skills/`, while root-level overview files keep the repository easy to browse for non-authors.
