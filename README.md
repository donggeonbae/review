# review

Structured paper reviews for the donggeonbae research system.

Use this repository to evaluate papers, extract evidence, compare methods, and prepare review artifacts that can later support writing projects.

## Related Repositories

- `donggeonbae/research`: shared source material and reusable research notes.
- `donggeonbae/review`: paper reviews and critique.
- `donggeonbae/figure`: paper figure generation and visual assets.
- `donggeonbae/writing`: LaTeX manuscript drafting and submission preparation.

## Suggested Workflow

1. Start from source notes in `donggeonbae/research`.
2. Create a review under `reviews/<topic>/<source-slug>.md`.
3. Extract key claims, methods, evidence, limitations, and open questions.
4. Link review conclusions to relevant figure work in `donggeonbae/figure` or writing projects in `donggeonbae/writing`.

## Suggested Folders

- `reviews/`
- `comparisons/`
- `evidence/`
- `replication/`
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

