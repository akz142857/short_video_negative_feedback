# Short-Video Negative Feedback Paper Draft

This folder contains a complete paper draft based on the deterministic
short-video experiment results in:

- `examples/experiment/short_video_negative_feedback/output/README.md`

## Files

- `paper_en.md`: Full English manuscript draft in Markdown.
- `paper_zh.md`: Chinese manuscript draft.
- `latex/main.tex`: LaTeX manuscript draft.
- `latex/references.bib`: BibTeX entries used by the LaTeX draft.
- `data/`: Lightweight experiment artifacts (CSVs, reports, figures) cited in
  the paper. See `data/README.md` for layout.
- `submission_package/`: Paper-focused files prepared for review submission.

## Data and Raw Logs

Raw SQLite event logs (`*.db`) are hosted on Google Drive to keep the
repository lean:

https://drive.google.com/drive/folders/1gp02IHtAbFy6tPns32lNMWcKmGJ-j-gQ?usp=drive_link

The Drive copy additionally includes the `batch_output_300_600_400/` large-scale
sweep (~3.8 GB) that is not needed to reproduce the paper claims but is
provided for completeness.

## Build (LaTeX)

From repository root:

```bash
cd docs/paper/short_video_negative_feedback/latex
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
```

