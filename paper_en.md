# Negative Feedback and Reach in Short-Video Recommendation:
# A Deterministic OASIS Study

## Abstract

We study whether explicit negative feedback can reduce the reach of low-quality
content in a short-video recommender. Using OASIS, we first run a deterministic
two-condition TikTok-style simulation (baseline vs. stronger
`not_interested` treatment) to verify mechanism behavior: platform-level totals
stay stable while the target video's negative feedback increases and its traffic
pool level decreases. We then run a larger four-arm robustness study (18
parameter configurations x 30 paired runs, with scaled creators/viewers/videos).
At larger scale, treatment robustly increases target negative-feedback metrics
(18/18 significant), while pool-level demotion remains directionally negative
but statistically weaker (3/18 significant). The results support explicit
negative feedback as a meaningful governance signal, with effect size and
significance depending on regime and scale.

## 1. Introduction

Negative-feedback controls such as "not interested" are widely deployed in
short-video products, but their direct effect is hard to isolate in live
systems. Online traffic is noisy, policies co-evolve, and product experiments
must trade off rigor against operational risk.

We use agent-based simulation to study the mechanism under controlled
conditions. OASIS provides platform actions, recommendation components, and
replayable experiment pipelines, which makes it suitable for this kind of
counterfactual comparison.

The scope of this paper is intentionally limited: we test whether increasing
explicit negative feedback on one low-quality item changes its distribution
level, and whether that change appears with stable platform-level totals.

Concretely, we contribute:

1. A deterministic two-condition protocol for short-video feedback analysis.
2. A clean controlled result showing target-item demotion (`traffic_pool_level: 1 -> 0`).
3. Reproducible artifacts (DBs, reports, and comparison outputs) for extension.

## 2. Related Work

Recent short-video recommendation studies explicitly model passive-negative
feedback (e.g., skip behavior) and use it as a supervision signal in sequential
recommendation models (Pan et al., 2023; arXiv:2308.04086). That line of work
is mainly offline and model-centric, with evaluation on logged interaction
datasets.

Our paper is complementary. We focus on intervention effects in a controlled
simulation: under matched baseline/treatment conditions, what distribution
changes follow from stronger explicit negative feedback on a target low-quality
item? This is a policy-effect question rather than a ranking-accuracy question.

## 3. Method

### 3.1 Environment

We use the TikTok-style mode in OASIS with traffic-pool recommendation. The run
contains 3 creators, 6 viewers, and 4 uploaded videos (dance, tech, comedy, and
lifestyle). Agents perform watches, comments, shares, and negative feedback
(`not_interested`). Livestream actions are enabled but are not primary outcome
variables in this study.

### 3.2 Experimental Design

We construct two deterministic conditions:

- **Baseline:** weak negative feedback against one low-quality comedy video.
- **Treatment:** stronger negative feedback against the same target video.

All non-treatment factors are identical: user identities, follow graph, upload
sequence, viewer plans, ranking parameters, and simulation step progression.
The only intervention is additional negative feedback events on the comedy item
in treatment.

### 3.3 Metrics

We track both platform-level and target-level metrics.

- Platform-level:
  - `total_views`
  - `avg_watch_ratio`
- Target video (low-quality comedy):
  - `negative_count`
  - `traffic_pool_level`

## 4. Experimental Setup and Reproducibility

### 4.1 Execution Pipeline

The pipeline runs with:

1. Generate baseline/treatment databases via:
   `examples/experiment/short_video_negative_feedback/run_experiment.py`
2. Generate per-run markdown summaries:
   `visualization/short_video_simulation/code/generate_report.py`
3. Generate cross-run comparison:
   `visualization/short_video_simulation/code/compare_runs.py`

### 4.2 Produced Artifacts

Key files:

- `negative_feedback_baseline.db`
- `negative_feedback_treatment.db`
- `baseline_report.md`
- `treatment_report.md`
- `comparison/comparison_time_series.csv`
- `comparison/comparison_metrics.png`

## 5. Results

### 5.1 Main Aggregate Results (Single-Run)

| Metric | Baseline | Treatment |
| --- | ---: | ---: |
| total_views | 16 | 16 |
| avg_watch_ratio | 0.638 | 0.638 |
| target negative_count | 1 | 3 |
| target traffic_pool_level | 1 | 0 |

### 5.2 Time-Series Evidence

The aggregate table is consistent with the run-level trajectory in the
comparison output. Figure 1 shows three time-series metrics generated directly
from the experiment artifacts: cumulative views, average watch ratio, and
average traffic-pool level.

![Figure 1: Baseline vs. treatment trajectories for views, watch ratio, and traffic-pool level.](/Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/output/comparison/comparison_metrics.png)

The divergence appears at the low-quality comedy item update step: negative
feedback accumulates more strongly in treatment, and the item's pool level is
reduced. Outside the treated item, platform-level curves remain close, matching
the interpretation that this intervention is selective rather than globally
disruptive.

### 5.3 Multi-Run Statistical Results (n=30)

To improve robustness, we ran 30 paired baseline/treatment experiments with
seeded perturbations (`watch_jitter=0.08`, `behavior_flip_prob=0.05`,
`treatment_extra_neg_prob=0.85`). We report paired differences and two-sided
paired sign-flip p-values.

| Metric | Paired Diff Mean (Treatment - Baseline) | 95% CI | p-value |
| --- | ---: | ---: | ---: |
| total_negative_feedback | +1.700 | [1.372, 2.028] | 0.00005 |
| comedy_negative_count | +1.767 | [1.613, 1.921] | 0.00005 |
| comedy_traffic_pool_level | -0.667 | [-0.862, -0.471] | 0.00005 |
| avg_watch_ratio | -0.00068 | [-0.00445, 0.00308] | 0.72296 |
| total_shares | -0.100 | [-0.355, 0.155] | 0.60457 |

These multi-run results strengthen the mechanism claim: treatment consistently
increases negative feedback and lowers the target comedy video's traffic-pool
level, while global engagement-style metrics show no statistically meaningful
shift under this setup.

### 5.4 Large-Scale Parameter Sweep (18 Configs x 30 Runs, Four-Arm Setup)

We then increase experimental strength with a four-arm setup (`baseline`,
`treatment`, `none`, `random`) and larger simulated scale (`3x` creators, `5x`
viewers, `4x` videos). For the treatment-vs-baseline comparison, we keep the
same 18-configuration grid:

- `watch_jitter in {0.04, 0.08, 0.12}`
- `behavior_flip_prob in {0.02, 0.05}`
- `treatment_extra_neg_prob in {0.70, 0.85, 1.00}`

Main robustness pattern under this larger setup:

- `comedy_negative_diff_mean > 0` and `p <= 0.05` in 18/18 configs.
- `comedy_pool_diff_mean` is directionally negative on average (`-0.087`) but
  only significant in 3/18 configs.
- Platform-level `watch_ratio` and `shares` remain stable (0/18 significant).

| treatment_extra_neg_prob | Mean comedy_pool_diff | SD | Significant configs (pool) | Mean comedy_negative_diff | SD | Significant configs (negative) |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| 0.70 | -0.061 | 0.039 | 0/6 | +1.339 | 0.071 | 6/6 |
| 0.85 | -0.083 | 0.072 | 1/6 | +1.567 | 0.060 | 6/6 |
| 1.00 | -0.117 | 0.084 | 2/6 | +1.922 | 0.046 | 6/6 |

The treatment-intensity trend remains monotonic at aggregate level: higher
`treatment_extra_neg_prob` yields stronger negative-feedback accumulation and
more negative (though modest) target pool-level shifts.

### 5.5 Control-Arms Comparison (vs Baseline)

To verify that results are not explained by arbitrary noise injections, we
compare three non-baseline strategies against baseline across the same 18
configurations:

| Condition vs Baseline | comedy_negative_count diff (mean ± sd) | comedy_traffic_pool_level diff (mean ± sd) | avg_watch_ratio diff (mean ± sd) | total_shares diff (mean ± sd) |
| --- | ---: | ---: | ---: | ---: |
| none | -5.339 ± 0.169 | +0.022 ± 0.040 | +0.000000 ± 0.000000 | +0.000 ± 0.000 |
| random | +0.700 ± 0.307 | +0.011 ± 0.044 | -0.000063 ± 0.000766 | +0.085 ± 0.724 |
| treatment | +1.609 ± 0.253 | -0.087 ± 0.068 | +0.000090 ± 0.000429 | +0.026 ± 0.351 |

This separation is informative: random negatives increase negative-count only
weakly and do not push pool-level downward, while targeted treatment delivers
the strongest increase in target negative feedback and the only consistently
negative pool-level direction.

![Figure 2: Large-scale four-arm robustness summary (18 configs x 30 paired runs).](/Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/batch_output_85plus/batch_85plus_fourarm_summary.png)

### 5.6 Mechanism Calibration: Balanced-Sensitive Profile (n=30)

To improve mechanism observability in the scaled setting, we introduced a
`balanced_sensitive` recommender profile that increases negative-feedback
penalty while avoiding the floor-effect observed in an overly aggressive
demotion profile. We then ran a paired 30-run probe (`20x` creators/viewers/videos,
`watch_jitter=0.30`, `behavior_flip_prob=0.10`,
`treatment_extra_neg_prob=1.00`).

| Metric | Paired Diff Mean (Treatment - Baseline) | p-value | Baseline Mean | Treatment Mean |
| --- | ---: | ---: | ---: | ---: |
| negative_feedback_rate | +0.005646 | 0.000050 | 0.151547 | 0.157193 |
| comedy_traffic_pool_level | -0.233333 | 0.015249 | 0.633333 | 0.400000 |
| retention_3s_rate | +0.000000 | 1.000000 | 0.982271 | 0.982271 |
| avg_watch_ratio | +0.000000 | 1.000000 | 0.622830 | 0.622830 |
| creator_coverage | +0.000000 | 1.000000 | 1.000000 | 1.000000 |

This calibration result closes an important gap in prior large-scale runs:
targeted negative feedback no longer changes only count-level signals; it now
produces statistically significant demotion at the target traffic-pool level.
At the same time, platform-level watch and coverage signals remain stable.

## 6. Discussion

The result is still useful but more nuanced at larger scale. Targeted explicit
negative feedback robustly increases item-level negative signals; pool-level
demotion remains sensitive to parameter regime. The new balanced-sensitive probe
shows that this sensitivity can be tuned into statistically significant target
demotion without destabilizing platform-level activity signals. This indicates
that intervention design and signal weighting matter jointly: negative feedback
is a strong governance signal, but ranking sensitivity must be calibrated.

## 7. Limitations

1. The simulation world is still small (fixed creators/viewers/categories) versus real platform scale.
2. Short horizon and limited content taxonomy.
3. No strategic adaptation from creators or viewers.
4. Findings demonstrate mechanism behavior, not production-scale effect sizes.

## 8. Ethics and Broader Impacts

This study uses synthetic agents and no personal user data. In real platforms,
negative-feedback-driven demotion can still produce fairness and representation
risks. Any deployment should pair such signals with calibration, monitoring, and
appeal mechanisms.

## 9. Conclusion

Under controlled conditions in OASIS, increasing explicit negative feedback on a
low-quality video reliably raises item-level negative-feedback metrics while
keeping platform totals stable. With the calibrated `balanced_sensitive`
profile, we also obtain statistically significant target pool-level demotion in
the scaled setting (`comedy_traffic_pool_level` diff `-0.233333`, `p=0.015249`).
This provides a stronger mechanism baseline for follow-up studies on longer
horizons and richer moderation/ranking policies.

## 10. Data and Reproducibility

All core artifacts are included in the repository output directory:

- Baseline DB:
  `examples/experiment/short_video_negative_feedback/output/negative_feedback_baseline.db`
- Treatment DB:
  `examples/experiment/short_video_negative_feedback/output/negative_feedback_treatment.db`
- Time-series CSV:
  `examples/experiment/short_video_negative_feedback/output/comparison/comparison_time_series.csv`
- Comparison figure:
  `examples/experiment/short_video_negative_feedback/output/comparison/comparison_metrics.png`
- Large-scale batch config summary CSV:
  `examples/experiment/short_video_negative_feedback/batch_output_85plus/batch_config_summary.csv`
- Large-scale batch report:
  `examples/experiment/short_video_negative_feedback/batch_output_85plus/batch_report.md`
- Balanced-sensitive n=30 probe summary:
  `examples/experiment/short_video_negative_feedback/output_metric_probe_balanced_n30/multirun_summary.csv`
- Balanced-sensitive n=30 probe script:
  `scripts/ci/run_short_video_metric_probe_balanced_n30.sh`
- Large-scale four-arm figure:
  `examples/experiment/short_video_negative_feedback/batch_output_85plus/batch_85plus_fourarm_summary.png`

Reproduction entry points:

1. `examples/experiment/short_video_negative_feedback/run_experiment.py`
2. `examples/experiment/short_video_negative_feedback/run_batch_experiments.py`
3. `visualization/short_video_simulation/code/generate_report.py`
4. `visualization/short_video_simulation/code/compare_runs.py`

## References

1. OASIS: Open Agent Social Interaction Simulations with One Million Agents. arXiv:2411.11581.
2. Covington, Adams, and Sargin. Deep Neural Networks for YouTube Recommendations. RecSys 2016.
3. Zhao et al. Recommending What Video to Watch Next: A Multitask Ranking System. RecSys 2019.
4. Rendle et al. BPR: Bayesian Personalized Ranking from Implicit Feedback. UAI 2009.
5. Park et al. Generative Agents: Interactive Simulacra of Human Behavior. UIST 2023.
6. Pan et al. Understanding and Modeling Passive-Negative Feedback for Short-video Sequential Recommendation. arXiv:2308.04086.
