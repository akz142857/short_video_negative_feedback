# 负反馈与短视频分发范围：
# 一项基于 OASIS 的确定性研究

## 摘要

本文研究一个具体问题：在短视频推荐系统中，显式负反馈是否能够降低低质量内容分发。我们在 OASIS 中先构建确定性两组对照（baseline vs. treatment）验证机制：在其他因素保持一致时，平台总体指标基本稳定，而目标视频负反馈上升、流量池层级下降。随后我们开展大规模四臂鲁棒性实验（18 组参数配置 × 每组 30 次配对运行，且扩大创作者/观众/视频规模）。结果显示：treatment 对目标负反馈指标提升在 18/18 配置显著；目标流量池层级呈负向趋势，但显著性较弱（3/18 配置显著）。该结果表明显式负反馈是有价值的治理信号，但其分发层级效果受参数与规模条件影响。

## 1. 引言

短视频平台通常通过“推荐优化”提升观看时长与互动率，但也可能放大低质量内容。现实系统普遍提供“不感兴趣”等显式负反馈入口，但其效果在真实线上环境中难以单独识别：流量噪声大、策略持续变化、线上实验风险高。

因此，我们采用可控的多智能体仿真方法。OASIS 提供了可复现实验流水线，支持用户行为、平台动作与推荐策略配置，适合做机制验证。本文聚焦于一个窄问题：仅增强某个低质量内容的负反馈信号，是否会改变其分发层级，同时保持平台总体指标稳定。

本文贡献如下：

1. 提供一个确定性、可复现的短视频负反馈对照实验协议。
2. 在受控条件下观察到目标内容分发层级下降（`traffic_pool_level: 1 -> 0`）。
3. 提供可复现实验产物（数据库、报告与对比结果），便于后续扩展研究。

## 2. 相关工作

已有短视频推荐研究已开始系统利用“被动负反馈”（例如划走/跳过行为）来
训练序列推荐模型（如 Pan et al., 2023, arXiv:2308.04086）。该方向主要
关注离线建模与预测性能，在真实日志数据上做模型效果比较。

本文与其形成互补：我们不是提出新的序列推荐模型，而是关注策略干预的因果
方向问题，即在匹配对照条件下，增强显式负反馈后，目标低质量内容的分发会
如何变化。换言之，本文研究的是“治理策略效果评估”，而非“离线排名精度提升”。

## 3. 方法

### 3.1 环境设置

实验采用 OASIS 的 TikTok 风格平台与 traffic-pool 推荐机制。仿真场景包含 3 位创作者、6 位观众、4 条视频（舞蹈、科技、喜剧、生活）。行为包括观看、评论、分享、负反馈（`not_interested`）。直播行为保留但不作为本文主指标。

### 3.2 对照设计

我们构建两组条件：

- **Baseline（基线）**：对目标低质量喜剧视频施加较弱负反馈。
- **Treatment（处理）**：对同一目标视频施加更强负反馈。

除上述差异外，其他因素完全一致：用户集合、关注关系、内容脚本、推荐参数、时间步与动作顺序。

### 3.3 评估指标

平台级指标：

- `total_views`
- `avg_watch_ratio`

目标视频级指标（低质量喜剧）：

- `negative_count`
- `traffic_pool_level`

## 4. 实验流程与复现

执行流程：

1. 使用 `run_experiment.py` 生成 baseline/treatment 两份数据库。
2. 使用 `generate_report.py` 生成单次运行报告。
3. 使用 `compare_runs.py` 生成跨条件对比结果。

关键产物：

- `negative_feedback_baseline.db`
- `negative_feedback_treatment.db`
- `baseline_report.md`
- `treatment_report.md`
- `comparison/comparison_time_series.csv`
- `comparison/comparison_metrics.png`

## 5. 实验结果

| 指标 | Baseline | Treatment |
| --- | ---: | ---: |
| total_views | 16 | 16 |
| avg_watch_ratio | 0.638 | 0.638 |
| 目标视频 negative_count | 1 | 3 |
| 目标视频 traffic_pool_level | 1 | 0 |

下图给出了基线组与处理组在时间维度上的对比轨迹（累计观看量、平均完播比、平均流量池层级）：

![图 1：Baseline 与 Treatment 的时间序列对比（views、watch ratio、traffic-pool level）](/Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/output/comparison/comparison_metrics.png)

结果表明：处理组并未改变平台总体指标，但使目标低质量视频被更明显地下调分发层级。在确定性对照条件下，该差异可归因于新增负反馈事件，而非随机波动。

### 5.1 多轮统计结果（n=30）

为了提升实验强度，我们进一步运行了 30 组配对 baseline/treatment 实验，
并引入可控扰动（`watch_jitter=0.08`、`behavior_flip_prob=0.05`、
`treatment_extra_neg_prob=0.85`）。采用双侧配对 sign-flip 随机化检验。

| 指标 | 配对差值均值（Treatment - Baseline） | 95% CI | p-value |
| --- | ---: | ---: | ---: |
| total_negative_feedback | +1.700 | [1.372, 2.028] | 0.00005 |
| comedy_negative_count | +1.767 | [1.613, 1.921] | 0.00005 |
| comedy_traffic_pool_level | -0.667 | [-0.862, -0.471] | 0.00005 |
| avg_watch_ratio | -0.00068 | [-0.00445, 0.00308] | 0.72296 |
| total_shares | -0.100 | [-0.355, 0.155] | 0.60457 |

这组多轮结果显著增强了结论可信度：处理组稳定提高了负反馈并显著降低目标喜剧视频流量池层级，而全局观看质量与分享等平台级指标未出现统计显著变化。

### 5.2 大规模参数扫描（18 组配置 × 每组 30 次，四臂设计）

我们将实验进一步增强为四臂设置（`baseline`、`treatment`、`none`、`random`），
并扩大仿真规模（创作者 `3x`、观众 `5x`、视频 `4x`）。在 treatment vs baseline
主比较中，仍使用 18 组参数网格：

- `watch_jitter in {0.04, 0.08, 0.12}`
- `behavior_flip_prob in {0.02, 0.05}`
- `treatment_extra_neg_prob in {0.70, 0.85, 1.00}`

在这套更强设置下，鲁棒性结果为：

- `comedy_negative_diff_mean > 0` 且 `p <= 0.05`：18/18。
- `comedy_pool_diff_mean` 平均为负（`-0.087`），但仅 3/18 组达到显著。
- 平台级 `watch_ratio` 与 `shares` 仍稳定（0/18 显著）。

| treatment_extra_neg_prob | comedy_pool_diff 均值 | 标准差 | pool 显著组数 | comedy_negative_diff 均值 | 标准差 | negative 显著组数 |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| 0.70 | -0.061 | 0.039 | 0/6 | +1.339 | 0.071 | 6/6 |
| 0.85 | -0.083 | 0.072 | 1/6 | +1.567 | 0.060 | 6/6 |
| 1.00 | -0.117 | 0.084 | 2/6 | +1.922 | 0.046 | 6/6 |

聚合趋势仍保持单调：`treatment_extra_neg_prob` 越高，目标内容负反馈累积越强，
分发层级差值越偏负，但在大规模噪声下其显著性弱于负反馈计数指标。

### 5.3 对照策略比较（相对 Baseline）

为了排除“任意扰动都有效”的可能，我们比较了三种非 baseline 策略：

| 条件（相对 Baseline） | comedy_negative_count 差值（均值 ± 标准差） | comedy_traffic_pool_level 差值（均值 ± 标准差） | avg_watch_ratio 差值（均值 ± 标准差） | total_shares 差值（均值 ± 标准差） |
| --- | ---: | ---: | ---: | ---: |
| none | -5.339 ± 0.169 | +0.022 ± 0.040 | +0.000000 ± 0.000000 | +0.000 ± 0.000 |
| random | +0.700 ± 0.307 | +0.011 ± 0.044 | -0.000063 ± 0.000766 | +0.085 ± 0.724 |
| treatment | +1.609 ± 0.253 | -0.087 ± 0.068 | +0.000090 ± 0.000429 | +0.026 ± 0.351 |

该对照结果说明：随机负反馈虽然会提高负反馈计数，但对分发层级几乎无定向抑制；
定向 treatment 在目标负反馈增幅与分发层级负向变化上都更强，机制解释更完整。

![图 2：大规模四臂鲁棒性汇总（18 组配置 × 每组 30 次）](/Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/batch_output_85plus/batch_85plus_fourarm_summary.png)

### 5.4 机制校准实验：Balanced-Sensitive 配置（n=30）

针对大规模设置下“分发层级信号弱”的问题，我们加入了 `balanced_sensitive`
推荐配置：提高负反馈惩罚权重，同时避免过强降级导致的地板效应。随后进行
30 组配对实验（`20x` 创作者/观众/视频，`watch_jitter=0.30`，
`behavior_flip_prob=0.10`，`treatment_extra_neg_prob=1.00`）。

| 指标 | 配对差值均值（Treatment - Baseline） | p-value | Baseline 均值 | Treatment 均值 |
| --- | ---: | ---: | ---: | ---: |
| negative_feedback_rate | +0.005646 | 0.000050 | 0.151547 | 0.157193 |
| comedy_traffic_pool_level | -0.233333 | 0.015249 | 0.633333 | 0.400000 |
| retention_3s_rate | +0.000000 | 1.000000 | 0.982271 | 0.982271 |
| avg_watch_ratio | +0.000000 | 1.000000 | 0.622830 | 0.622830 |
| creator_coverage | +0.000000 | 1.000000 | 1.000000 | 1.000000 |

该结果补齐了关键机制链路：定向负反馈不仅提升计数类信号，也在大规模条件下
显著传导到目标内容的流量池降级；同时平台级观看与覆盖信号仍保持稳定。

## 6. 讨论

该结果在大规模条件下呈现出更细化的结论：定向显式负反馈可以稳定提升目标内容
负反馈信号，且不明显影响平台级活跃指标；分发层级降级效应对参数更敏感。通过
`balanced_sensitive` 校准后，目标内容降级可达到统计显著，说明负反馈信号与
排序灵敏度需要联合设计。

## 7. 局限性

1. 仿真规模仍然较小（固定创作者/观众/内容类型），与真实平台规模存在差距。
2. 时间跨度较短，内容类型有限。
3. 未建模创作者策略性对抗行为。
4. 本文验证的是机制可行性，不代表线上真实规模效果大小。

## 8. 伦理与影响

本文仅使用仿真智能体，不涉及真实个人数据。尽管如此，现实部署中的负反馈降权仍可能带来公平性与代表性风险，后续应结合校准、监控与申诉机制进行治理设计。

## 9. 结论

在 OASIS 受控环境中，增强显式负反馈能够稳定提高目标内容的负反馈指标并保持
平台级指标稳定。进一步在 `balanced_sensitive` 配置下，我们在大规模条件中
获得了显著的目标流量池降级（`comedy_traffic_pool_level` 差值 `-0.233333`，
`p=0.015249`）。该流程可作为后续更长周期与更复杂治理策略研究的高复现基线。

## 10. 数据与复现入口

除单次与 30 次配对实验外，本文还使用了批量参数扫描产物：

- `examples/experiment/short_video_negative_feedback/batch_output_85plus/batch_config_summary.csv`
- `examples/experiment/short_video_negative_feedback/batch_output_85plus/batch_report.md`
- `examples/experiment/short_video_negative_feedback/batch_output_85plus/batch_85plus_fourarm_summary.png`
- `examples/experiment/short_video_negative_feedback/output_metric_probe_balanced_n30/multirun_summary.csv`

复现入口脚本：

1. `examples/experiment/short_video_negative_feedback/run_experiment.py`
2. `examples/experiment/short_video_negative_feedback/run_batch_experiments.py`
3. `visualization/short_video_simulation/code/generate_report.py`
4. `visualization/short_video_simulation/code/compare_runs.py`
5. `scripts/ci/run_short_video_metric_probe_balanced_n30.sh`

## 参考文献

1. OASIS: Open Agent Social Interaction Simulations with One Million Agents. arXiv:2411.11581.
2. Covington, Adams, and Sargin. Deep Neural Networks for YouTube Recommendations. RecSys 2016.
3. Zhao et al. Recommending What Video to Watch Next: A Multitask Ranking System. RecSys 2019.
4. Rendle et al. BPR: Bayesian Personalized Ranking from Implicit Feedback. UAI 2009.
5. Park et al. Generative Agents: Interactive Simulacra of Human Behavior. UIST 2023.
6. Pan et al. Understanding and Modeling Passive-Negative Feedback for Short-video Sequential Recommendation. arXiv:2308.04086.
