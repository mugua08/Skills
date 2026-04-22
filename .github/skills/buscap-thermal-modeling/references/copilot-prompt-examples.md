# Copilot 提问示例

## 目的

这份清单用于告诉团队成员：怎样向 Copilot 提问，才更容易命中当前 BusCap thermal modeling skill。

## 提问模板

推荐把问题写成下面这个结构：

```text
目标 + 输入路径 + 期望输出 + 是否需要 MATLAB/Simulink/batch
```

## 高命中关键词

如果问题里出现以下关键词，命中当前 skill 的概率更高：

- `thermal_model_export.mat`
- `buscap_nn_params.m`
- MATLAB
- Simulink
- DAT
- 单文件对比
- batch 对比
- 参数汇总
- `per_file_metrics.csv`
- 绘图

## 分组示例提示词

### 新同事

帮我把 `artifacts/iter_r2_verify/thermal_model_export.mat` 转成 MATLAB 可用的 `buscap_nn_params.m`，按当前仓库默认流程执行，并说明输出文件位置。

用 `INCA_Data/2026-04-03__变频表下边界25度.dat` 和 `artifacts/iter_r2_verify/thermal_model_export.mat` 跑一次 MATLAB 单步验证，帮我输出 summary 并说明误差是否合理。

基于 `INCA_Data/2026-04-03__变频表下边界25度.dat` 和 `artifacts/iter_r2_verify` 跑一次单文件 MATLAB / Simulink 对比，生成 CSV、JSON、MAT 和 compare 图。

### 回归验证

用 `artifacts/iter_r2_verify` 按当前默认参数重新生成 `buscap_nn_params.m`，然后选一个代表性 DAT 跑单文件 MATLAB / Simulink 回归，对比输出 summary 和 compare 图。

帮我导出当前 Simulink 运行实际使用到的参数到一个 `.m` 文件和一个 `.csv` 文件，方便我核对这次回归到底用了什么参数。

读取 `matlab/exports/batch_comparison/per_file_metrics.csv`，帮我生成 node2 总览图、Simulink-only 图和三节点总览图，用于版本回归对比。

### 批量评估

用 `artifacts/iter_r2_verify` 对 `INCA_Data` 全目录跑 batch MATLAB / Simulink 对比，把结果输出到 `matlab/exports/batch_comparison`。

帮我对 `INCA_Data` 跑 BusCap batch 对比，并重点汇总 `per_file_metrics.csv`、`batch_summary.json` 和 `batch_result.mat`。

读取 `matlab/exports/batch_comparison/per_file_metrics.csv`，帮我生成适合汇报的 batch 误差总览图。

### 排错

当前 Simulink 结果和 MATLAB 差异很大，请按这个仓库已有流程先帮我判断应该先查参数、输入 bundle 还是 fixed step 配置，不要直接发明新流程。

MATLAB 直放误差已经偏大，请先帮我检查应该优先验证参数版本、DAT 通道映射还是 `node4Mode`，先不要直接跑 batch。

batch 跑失败了，请先缩到单文件 `buscap_run_simulink_comparison` 复现问题，再告诉我最可能的阻塞点。

## 文档类提示词

基于当前仓库已有 BusCap skill，帮我写一份适合发飞书的说明文档，内容包含原理、常用命令、输出物和排错建议。

## 不推荐的提问方式

下面这类提问太泛，命中率会下降：

- 帮我看看这个模型
- 帮我跑一下仿真
- 帮我分析一下温度

问题不是不能回答，而是没有明确指出：

- 用 Python 还是 MATLAB / Simulink
- 输入文件是什么
- 目标是单文件、batch、参数导出还是绘图

## 最短版提示词

如果只想快速命中，可以直接抄下面几句：

- 帮我把 Python 导出的 `thermal_model_export.mat` 接到 MATLAB / Simulink 流程。
- 帮我对某个 DAT 文件跑 BusCap 单文件 MATLAB / Simulink 对比。
- 帮我对 `INCA_Data` 跑 BusCap batch 对比并输出 `per_file_metrics.csv`。
- 帮我导出当前 Simulink 使用参数并生成 batch 汇总图。

## 推荐优先顺序

- 新同事先用“生成参数脚本”或“单文件对比”类提示词
- 做版本回归优先用“回归验证”类提示词
- 做正式汇总优先用“批量评估”类提示词
- 出现异常先用“排错”类提示词，不要一上来就重跑全流程
