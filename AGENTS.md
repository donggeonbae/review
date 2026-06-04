# AGENTS.md

## Purpose

This repository is for structured paper review. Use it to evaluate academic papers, extract evidence, compare methods, and produce review artifacts that can support future manuscripts in `donggeonbae/writing`.

Related repositories:

- `donggeonbae/research`: shared source material, research maps, reading queues, datasets, and reusable notes.
- `donggeonbae/review`: structured paper reviews, evidence extraction, critique, and comparison.
- `donggeonbae/figure`: paper figures, diagrams, visual explanations, Figma assets, and image-generation workflows.
- `donggeonbae/writing`: LaTeX manuscript drafting, venue templates, citation integration, strict review loops, and submission preparation.
- `donggeonbae/presentation`: meeting decks, literature review decks, conference talks, posters, and speaker scripts.

## Repository Role

Use this repository for:

- single-paper reviews
- multi-paper comparison reviews
- method critiques
- evidence tables
- figure snapshot analysis
- replication notes
- reviewer-style comments
- review summaries that can be cited by writing projects
- HTML review reports that can be promoted into presentations

Do not use this repository as the main place for broad research maps, figure production, or manuscript drafts. Put those in `donggeonbae/research`, `donggeonbae/figure`, and `donggeonbae/writing`.

## Project Orientation

Before reviewing a paper:

1. Confirm the target paper, version, year, and source link.
2. Check `donggeonbae/research` for existing source notes.
3. Identify the review type: quick scan, detailed technical review, replication review, or comparative review.
4. Keep author claims, evidence, critique, and your interpretation clearly separated.
5. Capture or reference the paper's key figures and tables as figure snapshots whenever the source format permits it.
6. Plan the final deliverable as an HTML report first, then prepare a presentation handoff.

## Recommended Structure

- `reviews/`: Individual paper reviews grouped by topic.
- `comparisons/`: Multi-paper comparison notes.
- `evidence/`: Tables of claims, methods, datasets, metrics, and limitations.
- `snapshots/`: Paper figure/table snapshots used as visual evidence in reviews.
- `replication/`: Implementation, reproducibility, and experiment notes.
- `reports/`: Markdown sources for HTML review reports.
- `handoffs/`: Presentation handoffs derived from completed reviews.
- `docs/`: Cross-repository workflow and repository documentation.
- `templates/`: Reusable review templates.
- `scripts/`: Small maintenance or export scripts.

Update this structure if the repository develops a more specific convention.

## Review Standards

Every substantial review should include:

- full citation metadata
- research question or problem
- existing research context and core prior elements
- prior limitations or unresolved gaps the paper targets
- main contribution
- method summary connected to the targeted limitations
- dataset and experimental setup
- key results
- implications of the results
- implications of the paper for the broader research direction
- strengths
- limitations
- whether and how the paper resolves the prior limitations
- what limitations remain unresolved
- assumptions and threats to validity
- figure snapshot analysis tied to the paper's logic
- relevance to current donggeonbae writing projects
- links to source notes in `donggeonbae/research`

## Figure Snapshot Rules

Use figure snapshots actively. A review should not treat figures as decoration; it should use them as visual evidence for the paper's argument.

- Capture key figures, tables, pipeline diagrams, result plots, and ablation charts when the paper format allows it.
- Store snapshots under `snapshots/<topic-slug>/<source-slug>/`.
- Name snapshots by paper order and purpose, such as `fig-01-method-overview.png` or `table-02-main-results.png`.
- For each snapshot, record the source location: page, figure/table number, caption, and paper version.
- Explain what each snapshot proves, what it does not prove, and how it connects to the paper's logic.
- Prefer original paper visuals for review evidence. Use recreated diagrams only when the original cannot be captured or when a simplified explanation is explicitly needed.
- Do not alter a figure in a way that changes the scientific claim. If annotations are added, preserve the original snapshot separately.

## Logical Flow Requirements

Organize detailed reviews around the paper's own reasoning, not around a generic checklist.

The preferred narrative flow is:

1. Existing research core: what prior work already established.
2. Existing limitation: what bottleneck, gap, or unresolved issue remains.
3. Paper's central claim: what the authors say they contribute.
4. Limitation-resolution link: how the proposed method is supposed to address the gap.
5. Methodology: the actual mechanism, model, experiment, or theoretical move.
6. Results: what evidence the paper provides.
7. Result implication: what the results imply if valid.
8. Remaining limitation: what the paper still does not solve.
9. Broader implication: how this changes the research direction, writing project, or next experiment.

Every major section should make the connection explicit: `gap -> method -> evidence -> implication`.

## HTML Report Requirement

For substantial paper reviews, produce a report-ready Markdown file and build it into the repository's HTML archive framework.

Default locations:

```text
reports/<topic-slug>/<source-slug>.md
projects/<source-slug>/index.html
projects/<source-slug>/report.enc
```

Build command:

```powershell
$env:REPORT_PASSWORD="<local secret>"
node scripts/build-markdown-report.js --slug <source-slug> --input reports/<topic-slug>/<source-slug>.md --title "<Paper Title>"
```

If `REPORT_PASSWORD` is unavailable, still generate the transient plaintext HTML under `build/<source-slug>/report.html` for local review, but do not commit plaintext protected report bodies.

The HTML report should include:

- paper metadata
- figure snapshot map
- logical-flow review
- evidence table
- limitations and unresolved gaps
- presentation handoff section

## Evidence and Citation Rules

- Do not invent results, metrics, claims, or limitations.
- Mark missing information explicitly.
- Use short direct quotes only when exact wording matters.
- Prefer page, section, figure, or table references when available.
- Distinguish between `Authors claim`, `Observed evidence`, and `Reviewer interpretation`.

## Cross-Repository Interaction

Use stable research IDs to connect reviews with source notes and writing projects.

Recommended ID format:

```text
topic-slug/YYYY/source-slug
```

Examples:

```text
diffusion-policy/2023/chi-diffusion-policy
clinical-ai/2024/foundation-models-ehr
```

When a review depends on source notes, link back to `donggeonbae/research`. When a review suggests a figure, link forward to `donggeonbae/figure`. When a review supports a manuscript, link forward to `donggeonbae/writing`. When a review supports a literature review deck or talk, link forward to `donggeonbae/presentation`.

Prefer relative links when repositories are checked out under the same parent directory:

```md
Source note: ../research/sources/topic-slug/source-slug.md
Suggested figure: ../figure/figures/project-slug/figure-id/spec.md
Related manuscript: ../writing/manuscripts/project-slug/draft.md
Related presentation: ../presentation/literature-review/project-slug/deck.md
```

## Writing Style

- Be direct, analytical, and evidence-grounded.
- Separate summary from critique.
- Use tables for comparisons.
- Use concise bullets for strengths, weaknesses, and open questions.
- Avoid vague praise or vague criticism.

## Quality Checklist

Before finishing a review, verify:

- citation metadata is complete enough to identify the paper
- claims are tied to source evidence
- key figures or tables are captured or explicitly marked unavailable
- figure snapshots are interpreted, not merely inserted
- the paper's logic flow is visible from gap to method to evidence to implication
- critique is separated from summary
- limitations are concrete
- links to `research` and `writing` are included when relevant
- an HTML report build path is provided
- a presentation handoff is included when the review may become a deck
- open questions are listed

## Static HTML Archive Framework

This repository follows the source-derived encrypted static HTML archive pattern adapted from `Lukael/research`.

Framework files:

- `index.html`: public archive index.
- `styles/site.css`: shared dark archive styling.
- `scripts/site.js`: discovers `projects/<slug>/` folders through the GitHub Contents API or local directory listing.
- `scripts/decrypt-report.js`: unlocks `projects/<slug>/report.enc` in the browser using Web Crypto.
- `scripts/encrypt-report.js`: encrypts plaintext HTML into `report.enc` using `REPORT_PASSWORD`.
- `scripts/build-markdown-report.js`: builds a project unlock shell and optional encrypted report from Markdown.
- `scripts/build-3dgs-ri-report.js`: source-derived example builder kept for reference; prefer `build-markdown-report.js` for new work.
- `templates/unlock-template.html`: public password unlock shell.
- `templates/report-template.html`: dark two-column encrypted report body template.
- `projects/<slug>/`: public unlock shell plus encrypted payload for each protected report.

Do not commit plaintext protected report bodies under `projects/`. Use `build/` for transient plaintext output and keep encrypted payloads in `projects/<slug>/report.enc` when a report should be published.
## Agent Behavior

When acting as an AI review agent:

- Read for argument structure, evidence quality, and methodological soundness.
- Use figure snapshots as first-class evidence.
- Preserve the paper's logical sequence while making hidden assumptions explicit.
- Connect existing research, limitations, method, results, and implications into one coherent review narrative.
- Be careful with uncertainty and do not overstate conclusions.
- Prefer actionable critique over broad commentary.
- Produce an HTML-report-ready artifact for substantial reviews.
- Prepare a presentation handoff that can be used by `donggeonbae/presentation` to generate a PPTX and speaker script.
- Report what was reviewed, what evidence was extracted, what was built, and what still needs manual verification.



