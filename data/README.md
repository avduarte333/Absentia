# Authorization benchmark

The benchmark is an index of 30 disclosed broken access control advisories in 25 web applications. It contains no copies of the applications. Each record points to an upstream repository, a commit where the specified defect was present, and a commit that fixed it.

[`authz_instances.jsonl`](authz_instances.jsonl) is the full dataset and source of truth. It has one JSON object per line. [`instances.csv`](instances.csv) is a compact index derived from it for browsing; fields with longer explanations and source locations remain in the JSONL.

## Record fields

| Purpose | Fields |
| --- | --- |
| Identity and source | `id`, `repo`, `language`, `framework`, `advisory_url`, `fix_url` |
| Revisions | `vulnerable_commit`, `fixed_commit` |
| Authorization issue | `affected_routes`, `invariant`, `violation`, `expected_cwes`, `expected_categories`, `payload_types` |
| Source locations | `root_files`, `root_symbols`, `sink_files`, `sink_locations` |
| Matching guidance | `match_criteria`, `match_keywords` |

The `invariant` describes the access control property the route should enforce. The `violation` explains how the vulnerable version fails to enforce it. `sink_locations` gives line ranges in the vulnerable version associated with the fix. The matching fields help decide whether a detector's finding describes the *same disclosed issue*.

## Interpreting results

The evaluation unit is one advisory at its pinned vulnerable commit. A detector is credited when it identifies that advisory's defect; a paired result additionally requires that it no longer identify the defect at the pinned fixed commit.

This is a positive-only benchmark of known issues. It does not label every route in these applications as safe or vulnerable. Other findings in the same application should be investigated on their own merits rather than automatically counted as false positives.
