# 快速上手

## 目标

让第一次接触这个仓库的同事，在最短时间内完成以下动作：

1. 从 Python 导出参数接入 MATLAB
2. 跑通单文件 MATLAB / Simulink 对比
3. 跑通 batch 汇总

## 工作目录

先进入 MATLAB 目录：

```matlab
cd('g:/0000_CapTempEst/matlab')
```

## 默认参数

- `node4Mode = 'ntc_max'`
- `downsampleStep = 2`
- `rasterS = 0.2`
- `fixedStepS = 0.002`

## 最常用命令

### 1. 更新参数脚本

```matlab
buscap_generate_nn_params( ...
    'g:/0000_CapTempEst/artifacts/iter_r2_verify/thermal_model_export.mat', ...
    'g:/0000_CapTempEst/matlab/buscap_nn_params.m');
```

### 2. 单文件完整对比

```matlab
result = buscap_run_simulink_comparison( ...
    'g:/0000_CapTempEst/INCA_Data/2026-04-03__变频表下边界25度.dat', ...
    'g:/0000_CapTempEst/artifacts/iter_r2_verify', ...
    'buscap_thermal_network_v2025b');
```

### 3. 批量对比

```matlab
batchResult = buscap_batch_simulink_comparison( ...
    'g:/0000_CapTempEst/INCA_Data', ...
    'g:/0000_CapTempEst/artifacts/iter_r2_verify', ...
    'g:/0000_CapTempEst/matlab/exports/batch_comparison', ...
    'buscap_thermal_network_v2025b_batch', ...
    'ntc_max', 2, 0.2, 0.002, false);
```

### 4. 导出参数汇总

```matlab
outputPaths = buscap_export_simulink_params_summary('g:/0000_CapTempEst/matlab');
```

## 什么时候分别用哪个入口

- 只想看数据准备：`buscap_extract_signals`
- 只想看 MATLAB 真值回放：`buscap_validate_matlab_model`
- 想看单文件完整对比：`buscap_run_simulink_comparison`
- 想看全量结果：`buscap_batch_simulink_comparison`
- 想更新 MATLAB 参数：`buscap_generate_nn_params`
- 想导出参数表：`buscap_export_simulink_params_summary`
