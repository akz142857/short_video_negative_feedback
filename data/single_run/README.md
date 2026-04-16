# Short-Video Negative Feedback Experiment

This experiment is a deterministic template for a paper-style short-video study in OASIS.
It compares two otherwise identical TikTok-style runs:

- `baseline`: weak negative feedback against a low-quality comedy video
- `treatment`: stronger `not_interested` signals against that same low-quality video

The intended research question is whether explicit negative feedback suppresses reach in a traffic-pool recommender.

## Baseline

- Database: `/Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/output/negative_feedback_baseline.db`
- Total views: 16
- Total shares: 7
- Total negative feedback: 1
- Average watch ratio: 0.638
- Average traffic pool level: 1.000

| post_id | category | view_count | share_count | negative_count | traffic_pool_level |
| --- | --- | --- | --- | --- | --- |
| 1 | dance | 4 | 2 | 0 | 2 |
| 2 | tech | 4 | 2 | 0 | 1 |
| 3 | comedy | 4 | 2 | 1 | 1 |
| 4 | lifestyle | 4 | 1 | 0 | 0 |

## Treatment

- Database: `/Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/output/negative_feedback_treatment.db`
- Total views: 16
- Total shares: 7
- Total negative feedback: 3
- Average watch ratio: 0.638
- Average traffic pool level: 1.000

| post_id | category | view_count | share_count | negative_count | traffic_pool_level |
| --- | --- | --- | --- | --- | --- |
| 1 | dance | 4 | 2 | 0 | 2 |
| 2 | tech | 4 | 2 | 0 | 1 |
| 3 | comedy | 4 | 2 | 3 | 0 |
| 4 | lifestyle | 4 | 1 | 0 | 1 |

## Key Contrast

- Baseline low-quality comedy video traffic pool level: 1
- Treatment low-quality comedy video traffic pool level: 0
- Baseline low-quality comedy video negative feedback: 1
- Treatment low-quality comedy video negative feedback: 3

## Suggested Analysis Commands

```bash
python visualization/short_video_simulation/code/generate_report.py /Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/output/negative_feedback_baseline.db --output /Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/output/baseline_report.md
python visualization/short_video_simulation/code/generate_report.py /Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/output/negative_feedback_treatment.db --output /Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/output/treatment_report.md
python visualization/short_video_simulation/code/compare_runs.py baseline=/Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/output/negative_feedback_baseline.db treatment=/Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/output/negative_feedback_treatment.db --output-dir /Users/ziy/Code/MiroFishSpace/oasis/examples/experiment/short_video_negative_feedback/output/comparison
```
