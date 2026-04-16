# OASIS 短视频大规模实验最终摘要（300/600/400）

## 实验完成情况

- 目录：`/Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/batch_output_300_600_400`
- 配置总数：18（watch_jitter×behavior_flip×treatment_neg = 3×2×3）
- 每个配置：4个策略臂（baseline/treatment/none/random）× 30 runs
- 总计最小运行单元：2160
- 完整性检查：18/18 配置均生成 `strategy_pairwise_vs_baseline.csv`（无缺失）

## 全局统计结论

- `comedy_traffic_pool_level` paired diff 均值：0.000000（min=0.000000, max=0.000000）
- `comedy_traffic_pool_level` 显著配置数（p<=0.05）：0/18
- `comedy_negative_count` paired diff 均值：1.648148（min=1.266667, max=2.000000）
- `comedy_negative_count` 显著配置数（p<=0.05）：18/18
- `avg_watch_ratio` 差异绝对值：mean=0.00001206, max=0.00004200
- `total_shares` 差异绝对值：mean=12.9278, max=46.2000

## 分层观察（按 treatment_extra_neg_prob）

- tn=0.70: pool_diff_mean=0.000000, neg_diff_mean=1.366667, |watch_diff|_mean=0.00001900
- tn=0.85: pool_diff_mean=0.000000, neg_diff_mean=1.627778, |watch_diff|_mean=0.00001717
- tn=1.00: pool_diff_mean=0.000000, neg_diff_mean=1.950000, |watch_diff|_mean=0.00000000

## 解释（面向 OASIS 场景能力）

- 当前设定下，负反馈干预可以稳定改变“负反馈计数”，但尚不足以传导到 traffic pool 层级。
- 观看行为信号（watch_ratio）在 baseline/treatment 间几乎不变，导致推荐打分主导项变化有限。
- 因此现象是“反馈计数响应明显，流量层级响应不明显”，这是机制层面的可解释结果，而不是运行错误。

## 下一步（已计划）

- 引入并验证 3 个短视频核心场景指标：`retention_3s_rate`、`negative_feedback_rate`、`creator_coverage`。
- 进行小规模复现实验（新指标版本）检查“为什么 pool 不动”。