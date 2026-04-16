# Data and Experiment Artifacts

This directory contains the lightweight experiment artifacts cited in the paper:
CSV summaries, per-run Markdown reports, and figures. Raw SQLite event logs
(`*.db`) are **not** tracked in this repository — they are archived on Google
Drive along with the full 300/600/400 scale sweep.

## Google Drive (Full Dataset)

All experiment databases and raw event logs are available here:

https://drive.google.com/drive/folders/1gp02IHtAbFy6tPns32lNMWcKmGJ-j-gQ?usp=drive_link

The Drive copy mirrors the layout of the source `oasis-run/short_video_negative_feedback/`
directory and additionally includes the `batch_output_300_600_400/` large-scale
sweep (~3.8 GB, 72 SQLite DBs).

## Directory Map

| Path | Paper Section | Description | Size (repo) |
|------|---------------|-------------|-----:|
| `single_run/` | §5.1, §5.2 (Fig. 1) | Deterministic baseline vs. treatment single-run | 220 KB |
| `batch_85plus/` | §5.2, §5.3, §5.5 (Fig. 2) | 18-config × 30-run four-arm sweep (baseline/treatment/none/random) | 872 KB |
| `balanced_sensitive_n30/` | §5.6 | Balanced-sensitive profile paired n=30 probe (20x scale) | 28 KB |

## File Types (In-Repo)

Each run directory contains:

- `multirun_metrics.csv`, `multirun_summary.csv` — per-run and aggregated
  metric tables.
- `strategy_multirun_*.csv`, `strategy_pairwise_vs_baseline.csv` — four-arm
  comparison outputs.
- `MULTIRUN_REPORT.md`, `README.md` — human-readable summaries.

Top-level batch directories (`batch_85plus/`) additionally contain:

- `batch_config_summary.csv` — cross-configuration summary.
- `batch_report.md` — aggregated report across all 18 configs.
- `batch_85plus_fourarm_summary.png` — Fig. 2 in the paper.

## Files Kept Off-Repo

- `negative_feedback_{baseline,treatment,none,random}.db` — raw SQLite event
  logs. Download from Google Drive if you need to re-run analysis directly on
  event-level data.
- `batch_output_300_600_400/` — the 3.8 GB large-scale four-arm sweep (not
  cited in paper claims; included on Drive for completeness).

## Reproducing From Source

Raw databases can be regenerated from the OASIS experiment scripts listed in
the paper's §10 (Data and Reproducibility). The in-repo CSV summaries are
produced by the corresponding `generate_report.py` and `compare_runs.py`
pipelines after regeneration.
