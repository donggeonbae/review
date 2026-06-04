# AGENTS.md

## Purpose

This repository is for structured paper review. Use it to evaluate academic papers, extract evidence, compare methods, and produce review artifacts that can support future manuscripts in `Ramblue/writing`.

Related repositories:

- `Ramblue/research`: shared source material, research maps, reading queues, datasets, and reusable notes.
- `Ramblue/review`: structured paper reviews, evidence extraction, critique, and comparison.
- `Ramblue/figure`: paper figures, diagrams, visual explanations, Figma assets, and image-generation workflows.
- `Ramblue/writing`: LaTeX manuscript drafting, venue templates, citation integration, strict review loops, and submission preparation.
- `Ramblue/presentation`: meeting decks, literature review decks, conference talks, posters, and speaker scripts.

## Repository Role

Use this repository for:

- single-paper reviews
- multi-paper comparison reviews
- method critiques
- evidence tables
- replication notes
- reviewer-style comments
- review summaries that can be cited by writing projects

Do not use this repository as the main place for broad research maps, figure production, or manuscript drafts. Put those in `Ramblue/research`, `Ramblue/figure`, and `Ramblue/writing`.

## Project Orientation

Before reviewing a paper:

1. Confirm the target paper, version, year, and source link.
2. Check `Ramblue/research` for existing source notes.
3. Identify the review type: quick scan, detailed technical review, replication review, or comparative review.
4. Keep author claims, evidence, critique, and your interpretation clearly separated.

## Recommended Structure

- `reviews/`: Individual paper reviews grouped by topic.
- `comparisons/`: Multi-paper comparison notes.
- `evidence/`: Tables of claims, methods, datasets, metrics, and limitations.
- `replication/`: Implementation, reproducibility, and experiment notes.
- `docs/`: Cross-repository workflow and repository documentation.
- `templates/`: Reusable review templates.
- `scripts/`: Small maintenance or export scripts.

Update this structure if the repository develops a more specific convention.

## Review Standards

Every substantial review should include:

- full citation metadata
- research question or problem
- main contribution
- method summary
- dataset and experimental setup
- key results
- strengths
- limitations
- assumptions and threats to validity
- relevance to current Ramblue writing projects
- links to source notes in `Ramblue/research`

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

When a review depends on source notes, link back to `Ramblue/research`. When a review suggests a figure, link forward to `Ramblue/figure`. When a review supports a manuscript, link forward to `Ramblue/writing`. When a review supports a literature review deck or talk, link forward to `Ramblue/presentation`.

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
- critique is separated from summary
- limitations are concrete
- links to `research` and `writing` are included when relevant
- open questions are listed

## Agent Behavior

When acting as an AI review agent:

- Read for argument structure, evidence quality, and methodological soundness.
- Be careful with uncertainty and do not overstate conclusions.
- Prefer actionable critique over broad commentary.
- Report what was reviewed, what evidence was extracted, and what still needs manual verification.
