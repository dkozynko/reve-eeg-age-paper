# Origin and extraction provenance

Source research archive: https://github.com/dkozynko/neurobench_age

Source HEAD: `e6a1d9cdeffe2897f33b75c9bcdc9e0b58321688`. The extraction includes working-tree edits present on
September 21, 2026, so HEAD alone does not identify every copied byte.
[PROVENANCE.json](PROVENANCE.json) records the source and extracted SHA-256 of
every selected source file and marks scope/documentation adaptations.

This is a focused companion repository, not a new experiment or a claim of new
preregistration. Original scientific source-tree, checkpoint, prediction and
lock identities are preserved inside the unchanged result bundles. Extraction
hashes identify this delivery and must not be substituted for those original
execution identities.

## Included scope

Primary frozen REVE probes on MIPDB, training-size and layer-wise exploratory
extensions, and ds006780 v5 transfer. Included source code is the transitive
package dependency closure of the retained script entry points, plus HBN
manifest construction/download helpers and package initializers. Shared math,
preprocessing and independent-pipeline helpers remain even when their modules
also support older workflows. HBN source manifests, including the 500-subject
base of the nested selection, remain available for provenance.

## Deliberately omitted from this copy

- Historical fine-tuning, continued-pretraining and two-stage experiment paths.
- Old screening/finalist/layer-selection result bundles and their launchers.
- Tests specific to those omitted workflows.
- Unused font-test PDF and custom bibliography style.
- Editorial working notes and superseded implementation plans.

Those materials remain in the source repository. The manuscript preserves the
prior HBN R5 exposure and the exploratory status of follow-up analyses.
Source helpers and retained scientific results are copied without editing;
packaging entry points, paper availability wording and layout-specific tests
are adjusted for the focused scope. Original documentation that described all
tracks is updated to distinguish this extraction from the source archive.

## Delivery state

A new local Git repository is initialized without commits or remotes. No files
are published. Aggregate checks and manuscript builds work in this state;
sealing a fresh experiment requires a later author-managed clean commit.
Original raw EEG, predictions, caches and checkpoints are absent; recovering
cohort descriptors does not reconstruct them. No new software license has
been assigned. Before public release, choose the destination and update the
manuscript code link, which currently identifies the original research archive.

[VALIDATION.md](VALIDATION.md) records checks and environment limitations.
