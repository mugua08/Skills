# 输出物与产物目录

## 参数类产物

- `artifacts/.../thermal_model_export.mat`
  Python 导出的参数文件
- `matlab/buscap_nn_params.m`
  MATLAB 参数脚本
- `matlab/buscap_simulink_params_summary.m`
  Simulink 参数汇总 m 文件
- `matlab/buscap_simulink_params_summary.csv`
  Simulink 参数汇总 csv 文件

## 单文件产物

默认目录：`matlab/exports/comparison`

- `*_simulink_matlab_python_compare.csv`
- `*_simulink_matlab_python_summary.json`
- `*_simulink_matlab_python_result.mat`
- `*_simulink_matlab_python_compare.png`

## 批量产物

默认目录：`matlab/exports/batch_comparison`

- `per_file_metrics.csv`
- `batch_summary.json`
- `batch_result.mat`
- `per_file/` 子目录中的单文件产物

## 数据准备产物

默认目录：`matlab/exports`

- `*_prepared_timeseries.csv`
- `*_simulink_inputs.mat`

## 图像产物

常见位置：`matlab/exports/batch_comparison`

- `batch_t2_error_overview.png`
- `batch_t2_error_overview_simulink_only.png`
- `batch_all_nodes_error_overview.png`

## 如何判断这一步成功

- 参数更新成功：`buscap_nn_params.m` 被重写，MATLAB 无报错
- 单文件成功：comparison CSV / summary JSON / result MAT 至少三类文件落盘
- batch 成功：`per_file_metrics.csv`、`batch_summary.json`、`batch_result.mat` 同时存在
- 参数汇总成功：`buscap_simulink_params_summary.m` 与 csv 同时存在
