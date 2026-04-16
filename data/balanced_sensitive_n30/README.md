# Short-Video Negative Feedback Experiment

This experiment is a deterministic template for a paper-style short-video study in OASIS.
It compares two otherwise identical TikTok-style runs:

- `baseline`: weak negative feedback against a low-quality comedy video
- `treatment`: stronger `not_interested` signals against that same low-quality video

The intended research question is whether explicit negative feedback suppresses reach in a traffic-pool recommender.

## Baseline

- Database: `/Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/output_metric_probe_balanced_n30/negative_feedback_baseline.db`
- Total views: 6400
- Total shares: 2800
- Total negative feedback: 400
- Negative feedback rate: 0.0625
- Average watch ratio: 0.638
- Retention 3s rate: 1.0000
- Creator coverage: 1.0000
- Average traffic pool level: 0.887

| post_id | category | view_count | share_count | negative_count | traffic_pool_level |
| --- | --- | --- | --- | --- | --- |
| 1 | dance | 80 | 40 | 0 | 2 |
| 2 | tech | 80 | 40 | 0 | 1 |
| 3 | comedy | 80 | 40 | 20 | 1 |
| 4 | lifestyle | 80 | 20 | 0 | 0 |
| 5 | dance | 80 | 40 | 0 | 2 |
| 6 | tech | 80 | 40 | 0 | 1 |
| 7 | comedy | 80 | 40 | 20 | 1 |
| 8 | lifestyle | 80 | 20 | 0 | 0 |
| 9 | dance | 80 | 40 | 0 | 2 |
| 10 | tech | 80 | 40 | 0 | 1 |
| 11 | comedy | 80 | 40 | 20 | 1 |
| 12 | lifestyle | 80 | 20 | 0 | 0 |
| 13 | dance | 80 | 40 | 0 | 2 |
| 14 | tech | 80 | 40 | 0 | 1 |
| 15 | comedy | 80 | 40 | 20 | 1 |
| 16 | lifestyle | 80 | 20 | 0 | 0 |
| 17 | dance | 80 | 40 | 0 | 2 |
| 18 | tech | 80 | 40 | 0 | 1 |
| 19 | comedy | 80 | 40 | 20 | 1 |
| 20 | lifestyle | 80 | 20 | 0 | 0 |
| 21 | dance | 80 | 40 | 0 | 2 |
| 22 | tech | 80 | 40 | 0 | 1 |
| 23 | comedy | 80 | 40 | 20 | 1 |
| 24 | lifestyle | 80 | 20 | 0 | 0 |
| 25 | dance | 80 | 40 | 0 | 2 |
| 26 | tech | 80 | 40 | 0 | 1 |
| 27 | comedy | 80 | 40 | 20 | 1 |
| 28 | lifestyle | 80 | 20 | 0 | 0 |
| 29 | dance | 80 | 40 | 0 | 2 |
| 30 | tech | 80 | 40 | 0 | 1 |
| 31 | comedy | 80 | 40 | 20 | 1 |
| 32 | lifestyle | 80 | 20 | 0 | 0 |
| 33 | dance | 80 | 40 | 0 | 2 |
| 34 | tech | 80 | 40 | 0 | 1 |
| 35 | comedy | 80 | 40 | 20 | 1 |
| 36 | lifestyle | 80 | 20 | 0 | 0 |
| 37 | dance | 80 | 40 | 0 | 2 |
| 38 | tech | 80 | 40 | 0 | 1 |
| 39 | comedy | 80 | 40 | 20 | 1 |
| 40 | lifestyle | 80 | 20 | 0 | 0 |
| 41 | dance | 80 | 40 | 0 | 2 |
| 42 | tech | 80 | 40 | 0 | 1 |
| 43 | comedy | 80 | 40 | 20 | 1 |
| 44 | lifestyle | 80 | 20 | 0 | 0 |
| 45 | dance | 80 | 40 | 0 | 2 |
| 46 | tech | 80 | 40 | 0 | 1 |
| 47 | comedy | 80 | 40 | 20 | 1 |
| 48 | lifestyle | 80 | 20 | 0 | 0 |
| 49 | dance | 80 | 40 | 0 | 2 |
| 50 | tech | 80 | 40 | 0 | 1 |
| 51 | comedy | 80 | 40 | 20 | 1 |
| 52 | lifestyle | 80 | 20 | 0 | 0 |
| 53 | dance | 80 | 40 | 0 | 2 |
| 54 | tech | 80 | 40 | 0 | 1 |
| 55 | comedy | 80 | 40 | 20 | 1 |
| 56 | lifestyle | 80 | 20 | 0 | 0 |
| 57 | dance | 80 | 40 | 0 | 2 |
| 58 | tech | 80 | 40 | 0 | 1 |
| 59 | comedy | 80 | 40 | 20 | 0 |
| 60 | lifestyle | 80 | 20 | 0 | 0 |
| 61 | dance | 80 | 40 | 0 | 2 |
| 62 | tech | 80 | 40 | 0 | 1 |
| 63 | comedy | 80 | 40 | 20 | 0 |
| 64 | lifestyle | 80 | 20 | 0 | 0 |
| 65 | dance | 80 | 40 | 0 | 2 |
| 66 | tech | 80 | 40 | 0 | 1 |
| 67 | comedy | 80 | 40 | 20 | 0 |
| 68 | lifestyle | 80 | 20 | 0 | 0 |
| 69 | dance | 80 | 40 | 0 | 1 |
| 70 | tech | 80 | 40 | 0 | 1 |
| 71 | comedy | 80 | 40 | 20 | 0 |
| 72 | lifestyle | 80 | 20 | 0 | 0 |
| 73 | dance | 80 | 40 | 0 | 1 |
| 74 | tech | 80 | 40 | 0 | 1 |
| 75 | comedy | 80 | 40 | 20 | 0 |
| 76 | lifestyle | 80 | 20 | 0 | 0 |
| 77 | dance | 80 | 40 | 0 | 1 |
| 78 | tech | 80 | 40 | 0 | 1 |
| 79 | comedy | 80 | 40 | 20 | 0 |
| 80 | lifestyle | 80 | 20 | 0 | 0 |

## Treatment

- Database: `/Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/output_metric_probe_balanced_n30/negative_feedback_treatment.db`
- Total views: 6400
- Total shares: 2800
- Total negative feedback: 440
- Negative feedback rate: 0.0688
- Average watch ratio: 0.638
- Retention 3s rate: 1.0000
- Creator coverage: 1.0000
- Average traffic pool level: 0.887

| post_id | category | view_count | share_count | negative_count | traffic_pool_level |
| --- | --- | --- | --- | --- | --- |
| 1 | dance | 80 | 40 | 0 | 2 |
| 2 | tech | 80 | 40 | 0 | 1 |
| 3 | comedy | 80 | 40 | 22 | 0 |
| 4 | lifestyle | 80 | 20 | 0 | 1 |
| 5 | dance | 80 | 40 | 0 | 2 |
| 6 | tech | 80 | 40 | 0 | 1 |
| 7 | comedy | 80 | 40 | 22 | 0 |
| 8 | lifestyle | 80 | 20 | 0 | 1 |
| 9 | dance | 80 | 40 | 0 | 2 |
| 10 | tech | 80 | 40 | 0 | 1 |
| 11 | comedy | 80 | 40 | 22 | 0 |
| 12 | lifestyle | 80 | 20 | 0 | 1 |
| 13 | dance | 80 | 40 | 0 | 2 |
| 14 | tech | 80 | 40 | 0 | 1 |
| 15 | comedy | 80 | 40 | 22 | 0 |
| 16 | lifestyle | 80 | 20 | 0 | 1 |
| 17 | dance | 80 | 40 | 0 | 2 |
| 18 | tech | 80 | 40 | 0 | 1 |
| 19 | comedy | 80 | 40 | 22 | 0 |
| 20 | lifestyle | 80 | 20 | 0 | 1 |
| 21 | dance | 80 | 40 | 0 | 2 |
| 22 | tech | 80 | 40 | 0 | 1 |
| 23 | comedy | 80 | 40 | 22 | 0 |
| 24 | lifestyle | 80 | 20 | 0 | 1 |
| 25 | dance | 80 | 40 | 0 | 2 |
| 26 | tech | 80 | 40 | 0 | 1 |
| 27 | comedy | 80 | 40 | 22 | 0 |
| 28 | lifestyle | 80 | 20 | 0 | 1 |
| 29 | dance | 80 | 40 | 0 | 2 |
| 30 | tech | 80 | 40 | 0 | 1 |
| 31 | comedy | 80 | 40 | 22 | 0 |
| 32 | lifestyle | 80 | 20 | 0 | 1 |
| 33 | dance | 80 | 40 | 0 | 2 |
| 34 | tech | 80 | 40 | 0 | 1 |
| 35 | comedy | 80 | 40 | 22 | 0 |
| 36 | lifestyle | 80 | 20 | 0 | 1 |
| 37 | dance | 80 | 40 | 0 | 2 |
| 38 | tech | 80 | 40 | 0 | 1 |
| 39 | comedy | 80 | 40 | 22 | 0 |
| 40 | lifestyle | 80 | 20 | 0 | 1 |
| 41 | dance | 80 | 40 | 0 | 2 |
| 42 | tech | 80 | 40 | 0 | 1 |
| 43 | comedy | 80 | 40 | 22 | 0 |
| 44 | lifestyle | 80 | 20 | 0 | 1 |
| 45 | dance | 80 | 40 | 0 | 2 |
| 46 | tech | 80 | 40 | 0 | 1 |
| 47 | comedy | 80 | 40 | 22 | 0 |
| 48 | lifestyle | 80 | 20 | 0 | 1 |
| 49 | dance | 80 | 40 | 0 | 2 |
| 50 | tech | 80 | 40 | 0 | 1 |
| 51 | comedy | 80 | 40 | 22 | 0 |
| 52 | lifestyle | 80 | 20 | 0 | 1 |
| 53 | dance | 80 | 40 | 0 | 2 |
| 54 | tech | 80 | 40 | 0 | 1 |
| 55 | comedy | 80 | 40 | 22 | 0 |
| 56 | lifestyle | 80 | 20 | 0 | 1 |
| 57 | dance | 80 | 40 | 0 | 2 |
| 58 | tech | 80 | 40 | 0 | 1 |
| 59 | comedy | 80 | 40 | 22 | 0 |
| 60 | lifestyle | 80 | 20 | 0 | 0 |
| 61 | dance | 80 | 40 | 0 | 2 |
| 62 | tech | 80 | 40 | 0 | 1 |
| 63 | comedy | 80 | 40 | 22 | 0 |
| 64 | lifestyle | 80 | 20 | 0 | 0 |
| 65 | dance | 80 | 40 | 0 | 2 |
| 66 | tech | 80 | 40 | 0 | 1 |
| 67 | comedy | 80 | 40 | 22 | 0 |
| 68 | lifestyle | 80 | 20 | 0 | 0 |
| 69 | dance | 80 | 40 | 0 | 1 |
| 70 | tech | 80 | 40 | 0 | 1 |
| 71 | comedy | 80 | 40 | 22 | 0 |
| 72 | lifestyle | 80 | 20 | 0 | 0 |
| 73 | dance | 80 | 40 | 0 | 1 |
| 74 | tech | 80 | 40 | 0 | 1 |
| 75 | comedy | 80 | 40 | 22 | 0 |
| 76 | lifestyle | 80 | 20 | 0 | 0 |
| 77 | dance | 80 | 40 | 0 | 1 |
| 78 | tech | 80 | 40 | 0 | 1 |
| 79 | comedy | 80 | 40 | 22 | 0 |
| 80 | lifestyle | 80 | 20 | 0 | 0 |

## Key Contrast

- Baseline low-quality comedy video traffic pool level: 1
- Treatment low-quality comedy video traffic pool level: 0
- Baseline low-quality comedy video negative feedback: 20
- Treatment low-quality comedy video negative feedback: 22

## Suggested Analysis Commands

```bash
python visualization/short_video_simulation/code/generate_report.py /Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/output_metric_probe_balanced_n30/negative_feedback_baseline.db --output /Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/output_metric_probe_balanced_n30/baseline_report.md
python visualization/short_video_simulation/code/generate_report.py /Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/output_metric_probe_balanced_n30/negative_feedback_treatment.db --output /Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/output_metric_probe_balanced_n30/treatment_report.md
python visualization/short_video_simulation/code/compare_runs.py baseline=/Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/output_metric_probe_balanced_n30/negative_feedback_baseline.db treatment=/Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/output_metric_probe_balanced_n30/negative_feedback_treatment.db --output-dir /Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/output_metric_probe_balanced_n30/comparison
```
