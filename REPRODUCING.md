# Reproduction boundary

## Available from this repository

A clean checkout can validate aggregate artifact hashes, rerender the primary
and training-size presentation assets, build the manuscript and run synthetic
contract/regression tests. Relevant commands are in [README.md](README.md).
The original layer-wise and ds006780 bundles are retained with their manifests;
their asset builders and the layer-wise article audit are included.

The cohort recovery audit in
[docs/research/cohort_metadata_recovery_20260920.md](docs/research/cohort_metadata_recovery_20260920.md)
explains the HBN source-manifest match and ds006780 subject/age hash matches.
It does not claim to recover the training cache or rerun signal QC.

## Full experiment reruns

Follow [the execution contract](docs/research/article_ready_protocol.md),
[the training-size protocol](docs/research/capacity_data_regime_protocol.md),
and [the detailed reproduction guide](docs/research/reproduction.md).
Full runs need external datasets, the pinned REVE weights, and the appropriate
access-controlled inputs. Original participant-level predictions and execution
checkpoints are absent; recomputing metrics from those original predictions is
not possible using only this repository. A fresh run must preserve its own
inputs, manifests, predictions and checkpoints outside the public source tree.

The study-sealing code requires a committed HEAD and a clean working tree.
This extraction is deliberately delivered without commits, so aggregate
verification is available immediately, but sealing a new run requires the
author to create a clean committed snapshot first. Historical source-tree and
lock hashes describe the old experiment, not the extracted code tree. A new
run receives new provenance; do not overwrite historical evidence to make
new hashes appear to match old ones.

## Independent manuscript build

Run `make --directory=manuscript arxiv`. Extract `dist/arxiv-source.zip` into
an empty directory and run:

```bash
pdflatex -interaction=nonstopmode -halt-on-error main.tex
bibtex main
pdflatex -interaction=nonstopmode -halt-on-error main.tex
pdflatex -interaction=nonstopmode -halt-on-error main.tex
```

The archive includes only LaTeX dependencies and aggregate figure/table assets.
It does not include HBN participant rows, checkpoints or execution logs.
