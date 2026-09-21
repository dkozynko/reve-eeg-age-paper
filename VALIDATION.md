# Extraction validation — September 21, 2026

The final standalone repository, rather than only the staging copy, passed:

- **403 tests passed** in 132.77 seconds across 52 retained test modules.
- Package imports resolved inside the standalone repository's `src/` tree.
- All 241 recorded source/extraction and added-file identities matched.
- All 50 retained scientific source modules and 34 result/source-cohort files
  matched the research repository byte for byte.
- `uv lock --check --offline` passed; the unchanged lock resolves 142 packages.
- The layer-wise article audit passed with 75 participants, ten seeds and
  three comparisons, preserving the original analysis and asset identities.
- The manuscript verification/build completed: 18 pages, with no undefined
  references, missing font shapes or overfull boxes. The modified availability
  page was rendered and visually checked.
- The final 39-file arXiv archive compiled after extraction into a separate
  empty temporary directory. Text from all 18 pages exactly matched the PDF
  delivered in the standalone repository.
- Retained Markdown links and documented script/config/schema/result paths
  resolved. The original research archive remains separately attributed.
- The standalone Git repository has no commits and no remotes. Nothing was
  published, pushed or submitted.

## Environment and scope

Tests and rendering reused the existing Python 3.13.11 scientific environment
and local TeX installation. Import paths were checked to prevent importing
package code from the original checkout. A fresh network installation was not
performed; offline lock consistency was checked. Use the README's locked setup
commands when installing the separate project on another machine.

The first staging run exposed two tests for deliberately omitted historical
fine-tuning shell wrappers. Their three-test module was excluded together with
that old workflow; it contained no primary/extension scientific tests. The
final selected suite was rerun in full and passed. Layout and documentation
assertions were adapted to the new repository scope; scientific computation
code was not changed.

Validation is not a rerun of EEG inference or a recovery of missing predictions
and checkpoints. See REPRODUCING.md for that boundary and the clean-commit
requirement for sealing a future experiment.
