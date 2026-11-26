# Security Center integration contract — top-sites

## Audit snapshot
- The default branch is `main`.
- The Git tree contains ranked text datasets: `2k.txt`, `16k.txt`, `60k.txt`, `2kzipf.txt`, `uniform_filtered2k.txt`, `zipf1.5_filtered2k.txt`, and `zipf3_filtered2k.txt`.
- `generateurl.py` uses NumPy to sample rows; it accepts sample size, Zipf parameter, input path and output path.
- The repository has no README or conventional dependency manifest at its root. Dataset semantics, source provenance, refresh cadence, license and intended meaning of each variant are therefore not verified in this audit.

## Integration role
Treat this repository as an untrusted ranked-domain dataset, not as a verified allowlist or threat feed. Do not infer that a highly ranked domain is safe.

## Preview API contract
- `GET /v1/intel/top-sites/catalog` — list dataset identifiers and verified metadata only.
- `GET /v1/intel/top-sites/{dataset}` — serve a selected text dataset with a version/hash.
- Optional future lookup must be exact and read-only; no URL fetching or crawling from user-supplied targets.

## Blockers before activation
1. Add authoritative source URL, retrieval date, license and dataset schema for each file.
2. Explain why the variants exist and how ranks/sampling are produced.
3. Add validation for blank rows, duplicates, malformed domains and deterministic output.
4. Add a pinned NumPy dependency only if the generator remains part of the supported build.

Until these items are documented, this adapter remains disabled in Preview and datasets must not be used as reputation verdicts.
