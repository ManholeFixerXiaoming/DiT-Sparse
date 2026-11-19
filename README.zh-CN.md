# DiT-Sparse · 城市内涝预报结果

[English](README.md) | **简体中文**

本仓库展示 DiT-Sparse 项目在城市内涝（二维水动力）预报上的动画结果。目前只放 GIF，代码仍在整理与审核中，暂不开源。

所有动画统一为：**左：模型预报（Prediction）｜右：水动力模型实测（Observation）**，颜色表示水深（m），掩膜（计算域）以外为白色。

## 数据集一览

这些图片分为两个数据集：

| 数据集 | 区域 | 模型 | 测试事件 | 时长 |
| --- | --- | --- | --- | --- |
| 论文数据集 | tjyz、wjl | CA-Sparse（第 200 轮） | 526wd | 120 min |
| 深圳市数据集（U-RNN / UrbanFlood24） | Site 1–3 | GF-Dense（240 min 窗口） | r300y_p0.8_d3h | 360 min |

## 1. 论文数据集：tjyz 与 wjl

![tjyz / wjl](tjyz_wjl_demo/tjyz_wjl.gif)

同一场降雨（526wd，共 120 分钟）下两个区域的预报过程：上排 tjyz、下排 wjl。

| 区域 | 掩膜内 MAE (m) |
| --- | --- |
| tjyz | 0.0062 |
| wjl | 0.0115 |

- 水深色标：0 / 0.15 / 0.3 / 0.5 / 1 / 3 / 5 m，超过 5 m 按 5 m 显示。
- 120 帧，每帧 80 ms，循环播放。

## 2. 深圳市数据集（数据来源：U-RNN）

深圳的算例来自 [U-RNN](https://github.com/holmescao/U-RNN) 发布的 **UrbanFlood24** 数据集，对应三个场地（location1–3）。

GF-Dense 在每个场地上用 240 分钟降雨窗口（历史 159 分钟 + 当前 1 分钟 + 未来 80 分钟）从头训练 200 轮，取第 200 轮权重。测试事件为 300 年一遇设计暴雨 `r300y_p0.8_d3h`（峰值系数 0.8、3 小时雨型），共 360 分钟，降雨集中在前 180 分钟。

![Site 1](shenzhen_gf_dense/site1_gf_dense.gif)

| 场地 | 掩膜内 MAE (m) | 峰值 预报 / 实测 (m) |
| --- | --- | --- |
| Site 1 | 0.0044 | 2.16 / 2.16 |
| Site 2 | 0.0035 | 2.98 / 2.96 |
| Site 3 | 0.0034 | 2.05 / 2.09 |

![Site 2](shenzhen_gf_dense/site2_gf_dense.gif)

![Site 3](shenzhen_gf_dense/site3_gf_dense.gif)

- 水深色标：0 / 0.05 / 0.1 / 0.2 / 0.4 / 0.8 / 1.6 / 3.2 m。
- 每 3 分钟一帧，共 121 帧，每帧 70 ms，循环播放。

## 数据与代码可用性

- 深圳市数据集：[U-RNN](https://github.com/holmescao/U-RNN) 的 UrbanFlood24，使用时请遵循其许可。
- 论文数据集、模型权重，以及推理与绘图脚本：仍在整理审核中，暂不公开。
- 本仓库的 GIF 由内部脚本基于 Pillow 渲染，逐帧拼接预报与实测结果。

## 许可

本仓库的图片与文档仅限**学习、研究等非商业用途**，采用 [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/) 许可（全文见 [LICENSE](LICENSE)）：在署名且非商业的前提下，可以复制、传播和改编；**未经授权不得用于商业用途**。

商用授权与合作请联系：**qimingcheng@foxmail.com**。
