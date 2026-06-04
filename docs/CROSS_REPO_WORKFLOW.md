# Cross-Repository Workflow

The donggeonbae research system uses five repositories with distinct roles.

## Repositories

- `donggeonbae/research`: shared source material, research maps, reusable notes, and evidence.
- `donggeonbae/review`: structured paper reviews and comparative critique.
- `donggeonbae/figure`: paper figures, diagrams, visual explanations, Figma assets, and image-generation workflows.
- `donggeonbae/writing`: LaTeX manuscript drafts, venue templates, citation integration, strict review loops, and submission materials.
- `donggeonbae/presentation`: meeting decks, literature review decks, conference talks, posters, and speaker scripts.

## Review Flow

1. Use `research` to locate source metadata and reusable notes.
2. Create a structured review in `review`.
3. Extract claims, evidence, methods, limitations, and relevance.
4. Link review outputs to figure specs in `figure`, manuscript drafts in `writing`, or literature review decks in `presentation`.

## Shared ID Format

```text
topic-slug/YYYY/source-slug
```

## Link Convention

```md
Source note: ../research/sources/topic-slug/source-slug.md
Review: ../review/reviews/topic-slug/source-slug.md
Figure: ../figure/figures/project-slug/figure-id/spec.md
Manuscript: ../writing/manuscripts/project-slug/draft.md
Presentation: ../presentation/literature-review/project-slug/deck.md
```


