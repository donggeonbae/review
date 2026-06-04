# review

Structured paper reviews for the donggeonbae research system.

Use this repository to evaluate papers, extract evidence, compare methods, analyze figure snapshots, and prepare HTML review reports that can later support writing and presentation projects.

## Related Repositories

- `donggeonbae/research`: shared source material and reusable research notes.
- `donggeonbae/review`: paper reviews and critique.
- `donggeonbae/figure`: paper figure generation and visual assets.
- `donggeonbae/writing`: LaTeX manuscript drafting and submission preparation.
- `donggeonbae/presentation`: PPTX decks, posters, and speaker scripts.

## Suggested Workflow

1. Start from source notes in `donggeonbae/research`.
2. Capture key figure and table snapshots under `snapshots/<topic>/<source-slug>/`.
3. Create a review report under `reports/<topic>/<source-slug>.md`.
4. Connect prior research, prior limitations, method, results, result implications, remaining limitations, and broader implications in the paper's logical order.
5. Build the review into the encrypted HTML archive using `scripts/build-markdown-report.js`.
6. Create a presentation handoff for `donggeonbae/presentation` when the review should become a PPTX deck.

## Suggested Folders

- `reviews/`
- `comparisons/`
- `evidence/`
- `snapshots/`
- `replication/`
- `reports/`
- `handoffs/`
- `docs/`
- `templates/`
- `scripts/`


## HTML Archive Framework

This repository includes the encrypted static HTML archive framework adapted from `Lukael/research`.

Typical report flow:

```powershell
$env:REPORT_PASSWORD="<local secret>"
node scripts/build-markdown-report.js --slug example-report --input path\to\report.md --title "Example Report"
```

The command creates `projects/<slug>/index.html` and, when `REPORT_PASSWORD` is set, `projects/<slug>/report.enc`. The transient plaintext HTML is written under `build/` and should not be committed.

## Review-To-Presentation Flow

Use `templates/presentation-handoff.md` after the HTML report is complete. The handoff should identify:

- the presentation goal
- the paper's core logic flow
- the most important figure snapshots
- the slide sequence
- likely audience questions
- claims that require citation or manual verification

