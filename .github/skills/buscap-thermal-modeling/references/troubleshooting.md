# 排错清单

## 1. MATLAB 误差已经很大

优先检查：

1. 当前 `buscap_nn_params.m` 是否来自正确的 artifact
2. `thermal_model_export.mat` 是否是最新版本
3. DAT 通道是否匹配成功
4. `node4Mode` 是否仍为预期配置

优先执行：

```matlab
result = buscap_validate_matlab_model( ...
    'g:/0000_CapTempEst/INCA_Data/2026-04-03__变频表下边界25度.dat', ...
    'g:/0000_CapTempEst/artifacts/iter_r2_verify/thermal_model_export.mat');
```

## 2. MATLAB 正常但 Simulink 偏差大

优先检查：

1. `fixedStepS` 是否仍为 `0.002`
2. 输入 bundle 是否刚重新生成
3. Simulink wrapper 是否由最新脚本构建
4. 当前 Simulink block 是否仍通过 `buscap_interpreted_step` 调 `buscap_model_step`

## 3. batch 跑不通

优先做法：

1. 先缩到单文件 `buscap_run_simulink_comparison`
2. 确认单文件能落出结果
3. 再回到 batch

## 4. 怀疑 MATLAB 还在用旧参数

直接执行：

```matlab
buscap_generate_nn_params( ...
    'g:/0000_CapTempEst/artifacts/iter_r2_verify/thermal_model_export.mat', ...
    'g:/0000_CapTempEst/matlab/buscap_nn_params.m');
```

## 5. 参数汇总失败

优先检查：

1. `buscap_nn_params()` 是否能直接在 MATLAB 中返回 model struct
2. `buscap_model_step.m` 与 `build_buscap_simulink_skeleton.m` 是否在 MATLAB 路径中可见
