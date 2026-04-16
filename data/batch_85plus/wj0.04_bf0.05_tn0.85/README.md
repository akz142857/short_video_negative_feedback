# Short-Video Negative Feedback Experiment

This experiment is a deterministic template for a paper-style short-video study in OASIS.
It compares two otherwise identical TikTok-style runs:

- `baseline`: weak negative feedback against a low-quality comedy video
- `treatment`: stronger `not_interested` signals against that same low-quality video

The intended research question is whether explicit negative feedback suppresses reach in a traffic-pool recommender.

## Baseline

- Database: `/Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/batch_output_85plus/wj0.04_bf0.05_tn0.85/negative_feedback_baseline.db`
- Total views: 320
- Total shares: 140
- Total negative feedback: 20
- Average watch ratio: 0.637
- Average traffic pool level: 1.000

| post_id | category | view_count | share_count | negative_count | traffic_pool_level |
| --- | --- | --- | --- | --- | --- |
| 1 | dance | 20 | 10 | 0 | 2 |
| 2 | tech | 20 | 10 | 0 | 1 |
| 3 | comedy | 20 | 10 | 5 | 1 |
| 4 | lifestyle | 20 | 5 | 0 | 0 |
| 5 | dance | 20 | 10 | 0 | 2 |
| 6 | tech | 20 | 10 | 0 | 1 |
| 7 | comedy | 20 | 10 | 5 | 1 |
| 8 | lifestyle | 20 | 5 | 0 | 0 |
| 9 | dance | 20 | 10 | 0 | 2 |
| 10 | tech | 20 | 10 | 0 | 1 |
| 11 | comedy | 20 | 10 | 5 | 1 |
| 12 | lifestyle | 20 | 5 | 0 | 0 |
| 13 | dance | 20 | 10 | 0 | 2 |
| 14 | tech | 20 | 10 | 0 | 1 |
| 15 | comedy | 20 | 10 | 5 | 1 |
| 16 | lifestyle | 20 | 5 | 0 | 0 |

## Treatment

- Database: `/Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/batch_output_85plus/wj0.04_bf0.05_tn0.85/negative_feedback_treatment.db`
- Total views: 320
- Total shares: 140
- Total negative feedback: 28
- Average watch ratio: 0.637
- Average traffic pool level: 1.000

| post_id | category | view_count | share_count | negative_count | traffic_pool_level |
| --- | --- | --- | --- | --- | --- |
| 1 | dance | 20 | 10 | 0 | 2 |
| 2 | tech | 20 | 10 | 0 | 1 |
| 3 | comedy | 20 | 10 | 7 | 1 |
| 4 | lifestyle | 20 | 5 | 0 | 0 |
| 5 | dance | 20 | 10 | 0 | 2 |
| 6 | tech | 20 | 10 | 0 | 1 |
| 7 | comedy | 20 | 10 | 7 | 1 |
| 8 | lifestyle | 20 | 5 | 0 | 0 |
| 9 | dance | 20 | 10 | 0 | 2 |
| 10 | tech | 20 | 10 | 0 | 1 |
| 11 | comedy | 20 | 10 | 7 | 1 |
| 12 | lifestyle | 20 | 5 | 0 | 0 |
| 13 | dance | 20 | 10 | 0 | 2 |
| 14 | tech | 20 | 10 | 0 | 1 |
| 15 | comedy | 20 | 10 | 7 | 1 |
| 16 | lifestyle | 20 | 5 | 0 | 0 |

## Key Contrast

- Baseline low-quality comedy video traffic pool level: 1
- Treatment low-quality comedy video traffic pool level: 1
- Baseline low-quality comedy video negative feedback: 5
- Treatment low-quality comedy video negative feedback: 7

## Suggested Analysis Commands

```bash
python visualization/short_video_simulation/code/generate_report.py /Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/batch_output_85plus/wj0.04_bf0.05_tn0.85/negative_feedback_baseline.db --output /Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/batch_output_85plus/wj0.04_bf0.05_tn0.85/baseline_report.md
python visualization/short_video_simulation/code/generate_report.py /Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/batch_output_85plus/wj0.04_bf0.05_tn0.85/negative_feedback_treatment.db --output /Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/batch_output_85plus/wj0.04_bf0.05_tn0.85/treatment_report.md
python visualization/short_video_simulation/code/compare_runs.py baseline=/Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/batch_output_85plus/wj0.04_bf0.05_tn0.85/negative_feedback_baseline.db treatment=/Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/batch_output_85plus/wj0.04_bf0.05_tn0.85/negative_feedback_treatment.db --output-dir /Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/batch_output_85plus/wj0.04_bf0.05_tn0.85/comparison
```

## Additional Single-Run Controls

### none

- Database: `/Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/batch_output_85plus/wj0.04_bf0.05_tn0.85/negative_feedback_none.db`
- Total views: 320
- Total negative feedback: 0
- Comedy negative_count: 0
- Comedy traffic_pool_level: 1

### random

- Database: `/Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/batch_output_85plus/wj0.04_bf0.05_tn0.85/negative_feedback_random.db`
- Total views: 320
- Total negative feedback: 98
- Comedy negative_count: 7
- Comedy traffic_pool_level: 1
