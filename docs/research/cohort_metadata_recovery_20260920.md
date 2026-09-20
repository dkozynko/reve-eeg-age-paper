# Recovery of cohort descriptions

September 20, 2026. This audit corrects the earlier conclusion that the primary
HBN counts and selected ds006780 demographics could not be recovered. No model
was trained, no predictions were recomputed, and no retained result was changed.
The aggregate recovery output is in
[`cohort_metadata_recovery_20260920.json`](cohort_metadata_recovery_20260920.json).

## HBN: exact source-manifest identity

The Git-tracked file `results/canonical/data/age_medium_1000_nested.csv` exists
in HEAD and was introduced in commit `f022923`. Its SHA-256 is
`a5542dcbd49c0d6e0e591594c777bb66fb6cf80b61ac63f6639928d48225a7ac`, exactly
matching `provenance_evidence.hbn_subject_manifest` in the primary
`results/canonical/prospective/study_summary.json`.

| Split | Unique participants | Recordings | Age mean | Sample SD | Minimum | Maximum |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| Training | 800 | 800 | 10.173743 | 3.377077 | 5.0558 | 21.6740 |
| Validation | 100 | 100 | 10.168399 | 3.344101 | 5.0552 | 21.1761 |

Each split has one row per unique participant. Validation is release R8;
training is R1-R4, R6-R7 and R9-R10, with 100 participants per release. The
additional 100 R5 rows are the excluded historical test split. Counts were
computed from rows, not inferred from the filename or a secondary experiment.

The materialization implementation selects all `train`/`val` rows, rejects
duplicates, and records those subjects in the training manifest. The original
training-cache manifest itself was not recovered; this audit verifies its
source cohort, not its byte identity or execution cache. The retained summary's
`hbn_counts_retained: false` describes that summary and is not proof that the
source manifest is absent elsewhere in the repository. It is left unchanged
as historical evidence. Sex and diagnostic group are not fields in this CSV.

## ds006780: exact participant-list and target-vector matches

Public inputs were read from OpenNeuro version 1.0.0, source commit
`799d1502296ba5f74033734e149160c3d333e470`:

- [Pinned Git file tree](https://api.github.com/repos/OpenNeuroDatasets/ds006780/git/trees/799d1502296ba5f74033734e149160c3d333e470?recursive=1).
- [Participant table](https://raw.githubusercontent.com/OpenNeuroDatasets/ds006780/799d1502296ba5f74033734e149160c3d333e470/participants.tsv).
- [Field definitions](https://raw.githubusercontent.com/OpenNeuroDatasets/ds006780/799d1502296ba5f74033734e149160c3d333e470/participants.json).

The complete tree response was not truncated. Reconstruction followed the
repository's `PRIMARY_RECORDING_RE`: subject-level Restingstate run-01 BDF
files, requiring the matching channels, events and EEG JSON sidecars. There
were 129 matching recordings, of which one lacked its events file, leaving
128 candidates. The existing execution note in `external_replication_plan.md`
records that all 128 passed signal QC; this recovery did not rerun signal QC.

Joining candidates to the pinned participant table excluded one with no
participant row and one with no age. All remaining 126 ages were inside the
configured HBN support. Subjects were sorted by their UTF-8 byte order, and
ages were converted to floats in that order, exactly as in the analysis.
SHA-256 of the RFC 8785 canonical JSON arrays matched both retained values in
`results/extensions/ds006780_external_v5/external_analysis.json`:

| Identity | SHA-256 | Match |
| --- | --- | --- |
| Ordered subjects | `e71c351f4e941f49162a6f3be068a4cd5c3418f82048725432c27e01118f7aad` | exact |
| Ordered ages | `b24016fb9aa97d764d2a895de044ce3a15e3c2e00c3200ed5bb722efb0fb6878` | exact |

This identifies the original analysis population and age vector, rather than
merely producing a new sample of the same size. The downloaded participant
table has SHA-256
`4cd88d950e956bef9cf86c96db68e9be0ab6d30b4e9866b6dd184f2f1baa9838`.

| Selected-sample characteristic | Value |
| --- | ---: |
| Participants | 126 |
| Age mean / sample SD, years | 10.601587 / 1.572513 |
| Age range, years | 7.9-14.5 |
| Recorded male / female | 80 / 46 |
| Source group `TD` | 39 |
| Source group `ASD` | 62 |
| Source group `ASD SIBLING` | 25 |

Group labels above preserve the table's actual values. Its dictionary lists
`SIB`, while these rows use `ASD SIBLING`; no extra diagnosis was inferred.
The selected ages come from the hash-matched table and take precedence over
the source README's general 8-13-year description. The 136 metadata rows are
not the same starting inventory as the 129 run-01 recordings and should not be
presented as a simple 136-to-126 exclusion flow.

## Remaining limits

Family identifiers are absent from the inspected public schema. Family-aware
resampling remains unavailable; the participant-independence limitation stays
in the paper. This recovery does not reconstruct checkpoints, prediction
vectors, signal-QC reports, or the full execution manifests. It does resolve
the two previously identified sample-description gaps. Newly downloaded
participant rows remain outside the repository; only aggregates are added here.

Validation: 29 affected manuscript/documentation/release tests passed. The
updated PDF has 18 pages and was rendered for visual review. The 39-file arXiv
archive builds in an empty directory and yields exactly the same extracted
page text. All 61 previously fingerprinted result artifacts remain unchanged.
