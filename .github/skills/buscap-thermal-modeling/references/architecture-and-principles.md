# 架构与原理

## 当前主线模型

- 当前 MATLAB / Simulink 与 Python 主线一致，只保留 3 个网络：R、C、P
- 当前默认边界温度策略为 `ntc_max`
- R / C 网络输入 10 维
- P 网络输入 8 维
- 状态为 3 维：`T1, T2, T3`

## 为什么 MATLAB 和 Simulink 能共用一套核心

- `buscap_validate_matlab_model` 直接逐步调用 `buscap_model_step`
- Simulink 中的 MATLAB Function block 调用 `buscap_interpreted_step`
- `buscap_interpreted_step` 在 `dt > 0` 时再次调用 `buscap_model_step`

因此，MATLAB 直放与 Simulink 本质上共用同一套单步热模型计算核。

## 为什么 skill 以现有脚本为主而不是新建 wrapper

- 现有 MATLAB 脚本已经形成稳定闭环
- 单文件入口和 batch 入口已明确
- 参数汇总与绘图也已有固定产物格式
- 第一版 skill 的重点是可复用和可发现，而不是再设计一层新的命令封装

## 重要语义

- prepared 采样周期默认 `0.2 s`
- Simulink 固定步长默认 `0.002 s`
- 2 ms 信号对 prepared 特征做零阶保持
- `dt_s` 不是每个 2 ms 都非零，而是在状态更新边界打一拍
