---
name: buscap-thermal-modeling
description: 'Use for BusCap thermal model workflows: export Python thermal_model_export.mat to MATLAB buscap_nn_params.m, build Simulink models, run MATLAB replay, run single-file or batch MATLAB/Simulink comparison on DAT files, export parameter summaries, and plot batch comparison results. Keywords: Python MATLAB Simulink DAT batch comparison thermal model parameter summary plotting.'
argument-hint: 'Describe the goal, such as single-file validation, batch comparison, parameter export, or plotting.'
user-invocable: true
disable-model-invocation: false
---

# BusCap Thermal Modeling

## 何时使用

在以下场景加载本 skill：

- 需要把 Python 导出的模型参数接入 MATLAB / Simulink
- 需要生成 `buscap_nn_params.m`
- 需要基于 DAT 文件跑 MATLAB 直放验证
- 需要构建 Simulink wrapper 并运行仿真
- 需要做单文件 Python / MATLAB / Simulink 三方对齐
- 需要对整个 DAT 目录做 batch 对比
- 需要导出当前 Simulink 使用参数
- 需要生成 batch 结果汇总图

## 不做什么

- 不重新定义模型结构，默认复用当前仓库主线的 3NN 架构 R / C / P
- 不跳过现有入口脚本去发明新流程
- 不直接发布在线飞书页面；如需飞书内容，产出可复制的文稿

## 前置条件

在执行任何 MATLAB / Simulink 步骤前，先确认：

1. Python 已导出 `thermal_model_export.mat`
2. DAT 文件位于 `INCA_Data/`
3. 当前默认配置仍是：`node4Mode='ntc_max'`、`downsampleStep=2`、`rasterS=0.2`、`fixedStepS=0.002`
4. MATLAB 工作目录切到 `g:/0000_CapTempEst/matlab`

## 最短操作路径

### 路径 A：把 Python 模型接入 MATLAB / Simulink

1. 先生成 MATLAB 参数脚本：

```matlab
buscap_generate_nn_params( ...
    'g:/0000_CapTempEst/artifacts/iter_r2_verify/thermal_model_export.mat', ...
    'g:/0000_CapTempEst/matlab/buscap_nn_params.m');
```

2. 如果只想验证 MATLAB 模型本体：

```matlab
result = buscap_validate_matlab_model( ...
    'g:/0000_CapTempEst/INCA_Data/2026-04-03__变频表下边界25度.dat', ...
    'g:/0000_CapTempEst/artifacts/iter_r2_verify/thermal_model_export.mat');
```

3. 如果要构建 Simulink 并做单文件完整对比：

```matlab
result = buscap_run_simulink_comparison( ...
    'g:/0000_CapTempEst/INCA_Data/2026-04-03__变频表下边界25度.dat', ...
    'g:/0000_CapTempEst/artifacts/iter_r2_verify', ...
    'buscap_thermal_network_v2025b');
```

### 路径 B：做整个目录的正式评估

```matlab
batchResult = buscap_batch_simulink_comparison( ...
    'g:/0000_CapTempEst/INCA_Data', ...
    'g:/0000_CapTempEst/artifacts/iter_r2_verify', ...
    'g:/0000_CapTempEst/matlab/exports/batch_comparison', ...
    'buscap_thermal_network_v2025b_batch', ...
    'ntc_max', 2, 0.2, 0.002, false);
```

### 路径 C：导出参数归档并做图

1. 导出当前 Simulink 参数：

```matlab
outputPaths = buscap_export_simulink_params_summary('g:/0000_CapTempEst/matlab');
```

2. 生成 batch 汇总图：

```powershell
python plot_batch_comparison_summary.py --csv g:/0000_CapTempEst/matlab/exports/batch_comparison/per_file_metrics.csv
```

## 推荐执行顺序

1. Python 导出模型参数
2. MATLAB 生成 `buscap_nn_params.m`
3. 单文件检查数据准备与 MATLAB 直放
4. 单文件跑 Simulink 完整对比
5. 全量 DAT 跑 batch 对比
6. 导出参数汇总和批量图表

## 故障排查决策树

- 如果 MATLAB 误差已经很大，先检查参数版本和 DAT 通道映射，再跑 `buscap_validate_matlab_model`
- 如果 MATLAB 正常但 Simulink 偏差大，优先检查 `fixedStepS=0.002`、输入 bundle 是否刚生成、Simulink 模型是否由最新脚本重建
- 如果 batch 失败，先缩小到单文件 `buscap_run_simulink_comparison`
- 如果怀疑参数过期，重新运行 `buscap_generate_nn_params`

## 参考资料

- [快速上手](./references/quick-start.md)
- [Copilot 提问示例](./references/copilot-prompt-examples.md)
- [主流程细节](./references/workflow-details.md)
- [输出物与产物目录](./references/outputs-and-artifacts.md)
- [排错清单](./references/troubleshooting.md)
- [架构与原理](./references/architecture-and-principles.md)
- [绘图与报告](./references/plotting-and-reporting.md)

## 怎样向 Copilot 提问更容易命中这个 skill

优先在提问里显式写出以下关键词中的至少两个：

- Python 导出模型 / `thermal_model_export.mat`
- MATLAB 参数脚本 / `buscap_nn_params.m`
- Simulink 模型 / wrapper / 仿真
- 单文件对比 / batch 对比 / DAT 文件
- 参数汇总 / 绘图 / `per_file_metrics.csv`

更好的提问方式是“目标 + 输入路径 + 想要的输出”。

例如：

- 帮我把 `artifacts/iter_r2_verify/thermal_model_export.mat` 生成成 MATLAB 的 `buscap_nn_params.m`，并检查是否能被当前 Simulink 流程使用。
- 基于 `INCA_Data/某个文件.dat` 跑一次单文件 MATLAB / Simulink 对比，输出 summary 和 compare 图。
- 用 `artifacts/iter_r2_verify` 对 `INCA_Data` 全目录做 batch Simulink 对比，并汇总 `per_file_metrics.csv`。
- 导出当前 Simulink 使用参数到 `.m` 和 `.csv`，方便审查。
- 读取 `matlab/exports/batch_comparison/per_file_metrics.csv`，帮我生成 batch 总览图。
