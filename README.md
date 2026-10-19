# PhysicalAI-AV Text Annotations

基于 [NVIDIA PhysicalAI-Autonomous-Vehicles](https://huggingface.co/datasets/nvidia/PhysicalAI-Autonomous-Vehicles) 前视广角相机（`camera_front_wide_120fov`）视频，通过 Qwen3-VL 自动生成的中文文本标注。

本仓库提供逐帧和时间段两类标注。

## 数据内容

| 目录 | 内容 | JSON 文件数 |
| --- | --- | ---: |
| `frame_captions/` | 采样帧的场景概述与物体描述 | 19,497 |
| `temporal_events/` | 按事件划分的时间段描述，部分包含风险标签 | 19,517 |

共 **39,014 个 JSON 文件**，约 **237 MiB**。文件按 `chunk_0000` 至 `chunk_0200` 分块组织，通过文件名中的视频 UUID 对应原始视频；两类标注因失败记录过滤，不保证完全一一配对。

## 标注格式

- **逐帧标注**：`*_analysis.json`，包含 `analysis_metadata` 和 `frame_descriptions`；每帧主要包含 `timestamp`、`scene_overview`、`object_descriptions`。
- **时间段标注**：`*_adaptive_clip_analysis.json`，包含 `analysis_metadata` 和 `timeline_events`；每段主要包含 `time_segment`、`scene_description`，部分包含 `risk_tags`。

描述涵盖自车行为、周围车辆与行人、空间关系与交互、交通设施、天气与路面状况，以及潜在风险。

## 数据说明

标注生成于 2026 年 1 月。两类原始结果各有 19,536 个文件，发布时分别过滤：逐帧标注剔除 27 个报错文件和 12 个含失败占位描述的文件，保留 19,497 个；时间段标注剔除 19 个缺少有效 `timeline_events` 字段的文件，保留 19,517 个。因此，两类文件数量相差 20 个。共剔除 58 个文件，并移除了本地路径等元数据。

这些标注由模型自动生成，未经逐条人工核验，可能存在识别错误、风险推测和时间边界偏差。数据包含不同提示词版本，风险标签命名尚未完全统一，不应视为人工验证的真值标注。

原始数据归 NVIDIA 所有，获取和使用原始数据须遵守其许可条款。本仓库未另行授予开放许可证；公开可访问不代表获得原始数据或衍生标注的任意使用、再分发授权。
