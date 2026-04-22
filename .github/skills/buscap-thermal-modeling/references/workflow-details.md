# 主流程细节

## 主线闭环

### 阶段 1：Python 参数导出

Python 训练完成后，应先得到：

- `thermal_model_export.mat`
- 可选的 `temperature_predictions.csv`

当前 skill 默认复用仓库里已有 artifact，不强制重新训练。

### 阶段 2：生成 MATLAB 参数脚本

入口：`buscap_generate_nn_params`

输入：

- `thermal_model_export.mat`

输出：

- `buscap_nn_params.m`

说明：

- 这一步把 Python 导出的网络权重和归一化统计量固化成 MATLAB 可直接调用的函数

### 阶段 3：准备 DAT 输入

入口：`buscap_read_dat` 和 `buscap_prepare_simulink_input`

输入：

- `*.dat`
- `node4Mode`
- `downsampleStep`
- `rasterS`
- `fixedStepS`

输出：

- prepared table
- 2 ms fixed-step bundle

说明：

- `buscap_read_dat` 负责通道映射、重采样、边界温度选择
- `buscap_prepare_simulink_input` 负责把 prepared table 展开成 Simulink 所需的 11 维输入

### 阶段 4：MATLAB 单步直放验证

入口：`buscap_validate_matlab_model`

作用：

- 不经过 Simulink，直接验证模型本体是否合理

输出：

- `result.summary`
- `result.table`

### 阶段 5：构建 Simulink 模型并仿真

入口：`build_buscap_simulink_skeleton`

作用：

- 动态创建固定步长 Simulink wrapper
- 把参数、初始状态、stepInputs 注入 workspace
- 在 MATLAB Function block 内调用 `buscap_interpreted_step`

### 阶段 6：单文件完整对比

入口：`buscap_run_simulink_comparison`

内部顺序：

1. 重生成参数脚本
2. 读取 DAT
3. 生成 fixed-step 输入
4. 跑 MATLAB 直放
5. 构建并运行 Simulink
6. 对齐可选 Python 预测
7. 输出 CSV / JSON / MAT / PNG

### 阶段 7：批量对比

入口：`buscap_batch_simulink_comparison`

作用：

- 遍历全部 DAT 文件
- 逐文件调用单文件入口
- 汇总出 per-file 指标与 batch summary
