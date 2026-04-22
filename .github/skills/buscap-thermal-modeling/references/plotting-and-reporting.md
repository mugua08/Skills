# 绘图与报告

## 适用场景

- 已经跑完 batch 对比
- 想把 per-file 误差表转成总览图

## 输入文件

- `matlab/exports/batch_comparison/per_file_metrics.csv`

## 常用命令

```powershell
python plot_batch_comparison_summary.py --csv g:/0000_CapTempEst/matlab/exports/batch_comparison/per_file_metrics.csv
```

## 典型输出图

- `batch_t2_error_overview.png`
- `batch_t2_error_overview_simulink_only.png`
- `batch_all_nodes_error_overview.png`

## 结果解读建议

- 如果关注单个节点 2 的整体表现，先看 `batch_t2_error_overview.png`
- 如果只关心 Simulink 侧表现，先看 `batch_t2_error_overview_simulink_only.png`
- 如果想同时比较 T1 / T2 / T3 三节点，查看 `batch_all_nodes_error_overview.png`
