# Absentia

Absentia is a research project on finding broken access control vulnerabilities in web application source code. It maps an application's routes to the code behind them, then uses language model agents to infer what each route should allow and check whether the code enforces that property. The resulting findings are claims for a security reviewer to verify. The analysis reads source code; it does not run the application or send requests to it.

## Current release

This repository currently shares the [authorization benchmark](data/README.md). **We plan to upload the Absentia implementation by the end of 2026.**

The benchmark contains 30 publicly disclosed advisories from 25 open source web applications across nine frameworks: 18 Python, nine TypeScript, and three JavaScript cases. Each case links to the upstream project and advisory, identifies a vulnerable commit and a fixing commit, and describes the affected routes and the access control property at issue. Application source code stays in the upstream projects.

| File | Contents |
| --- | --- |
| [`data/authz_instances.jsonl`](data/authz_instances.jsonl) | Full benchmark records, one JSON object per advisory |
| [`data/instances.csv`](data/instances.csv) | Compact index for browsing the cases on GitHub or in a spreadsheet |
| [`data/README.md`](data/README.md) | Field descriptions and guidance for interpreting the benchmark |

## Approach and reported results

Absentia first maps the request surface of an application. It then reviews each route against an inferred authorization property and reports potential violations for human review. This procedure is intended to make the audit systematic across routes.

In the current evaluation of these 30 known vulnerabilities, Absentia reported 19 on the vulnerable commits. It reported 17 while also clearing the corresponding fixed commits. An unstructured agent using the same model reported three; CodeQL and Semgrep reported none of the 30. These are detection counts for the specified advisories, not a measure of how many other vulnerabilities or false positives exist in the applications.

The repository will gain the implementation and fuller reproduction instructions with the planned code release.
