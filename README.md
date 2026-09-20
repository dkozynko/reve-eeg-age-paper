# Cross-cohort EEG age prediction with frozen REVE

Companion code and retained evidence for **Do More Expressive Probes Improve
EEG Age Prediction? A Cross-Cohort Study with Frozen REVE**.

Dmytro Kozynko · Independent Researcher · dmytro.kozynko@gmail.com

This repository is a focused extraction of the
[original research archive](https://github.com/dkozynko/neurobench_age).
See [PROVENANCE.md](PROVENANCE.md) for the source revision, extraction boundary,
and file identities. This local repository has not been published or committed.

## Evidence included

| Analysis | Retained evidence | Interpretation |
| --- | --- | --- |
| Primary prospective study | 40 frozen-head runs, 75 MIPDB participants, 3,000 prediction identities | No tested head met the joint stable-improvement rule; this does not establish equivalence |
| Training-size extension | 200/400/800 HBN training subjects, three heads, ten seeds | Exploratory; reuses MIPDB |
| Layer-wise extension | Four REVE depths, ten seeds | Exploratory; reuses MIPDB |
| ds006780 v5 transfer | 126 participants, two heads, two training sizes | Separate secondary cohort; precision gate failed |

These are compact canonical evidence and aggregate artifacts, not the original
prediction vectors. Primary analysis identity:
`7747a16e11629164b524b2113ab2230d260012022fc46f68540c7f7578c2a3b6`.
Layer-wise analysis identity:
`f1f757ef53a8aad10615afd7fa0d6f8e2bc4e7f04ec33ce2d870f92e44706565`;
its asset-manifest identity:
`14b5afe5623f34fbaed4fcbe98ee8b59528769bf468bd1bcd83b941353a2be9d`.

## Quick start

Python 3.12+ and `uv` are required for the locked Python setup. A TeX distribution
with pdfLaTeX, BibTeX and Latin Modern is required to build the manuscript.

```bash
uv sync --frozen --extra test --extra manuscript
uv run --frozen --extra test --extra manuscript pytest -q
uv run --frozen --extra test python scripts/audit_layerwise_article.py
make --directory=manuscript arxiv
```

The final command builds `manuscript/main.pdf` and `dist/arxiv-source.zip`.
It does not download EEG or run model training. See
[REPRODUCING.md](REPRODUCING.md) for the distinction between rendering retained
results and rerunning participant-level inference.

## Layout

- `manuscript/`: article, references, tables, figures and build targets.
- `results/canonical/prospective/`: unchanged primary analysis bundle.
- `results/extensions/`: unchanged training-size, layer-wise and ds006780 bundles.
- `results/canonical/data/`: original HBN split manifests and identities.
- `src/neurobench_age/`, `scripts/`: retained experiment and analysis code.
- `configs/research/`, `schemas/`, `tests/`: protocols and validation.
- `docs/research/`: execution contracts, evidence registry and cohort recovery.

## Historical and data boundaries

Previously inspected HBN R5 results are retrospective secondary evidence and
must not be used for model or head selection or presented as untouched
confirmation. Historical fine-tuning and screening outputs remain in the
original research archive; the paper's exploratory analyses remain here.

The HBN source manifests contain participant identifiers, ages and split
membership. This existing source-cohort exception is documented explicitly.
Raw EEG, original participant-level predictions, execution caches and model
checkpoints are not included. They are not known to be available in a separate
archive. Hashes authenticate matching artifacts; they cannot reconstruct them.
The selected ds006780 description was recovered from pinned public metadata
with matching participant and age hashes; family links remain unknown.

Before publication, choose the public destination and update the manuscript's
code-availability link to it while retaining the original archive attribution.
The extraction does not assign a new software license or publish any files.
