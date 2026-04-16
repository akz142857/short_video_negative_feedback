# Short-Video Negative Feedback Paper Draft

This folder contains a complete paper draft based on the deterministic
short-video experiment results in:

- `examples/experiment/short_video_negative_feedback/output/README.md`

## Files

- `paper_en.md`: Full English manuscript draft in Markdown.
- `latex/main.tex`: LaTeX manuscript draft.
- `latex/references.bib`: BibTeX entries used by the LaTeX draft.

## Build (LaTeX)

From repository root:

```bash
cd docs/paper/short_video_negative_feedback/latex
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
```

