# Provenance

## Thread lineage (uber/ADR#163)

| date | author | event |
|---|---|---|
| 2026-10-08 | Aicent-com | proposal: portable offline-verifiable attestation for agent sessions (iqa-mcp) |
| 2026-10-21 | Paraphern | rugsnare introduced; ATTESTATION/VERDICT separation proposed; receipt-format comparison offered |
| 2026-10-22 | Aicent-com | accepted the comparison; proposed a field-level mapping; posted verified package numbers (rttp 1.3.1) |
| 2026-10-22 | Paraphern | four-row property skeleton; three-field minimal interchange; "Happy to co-draft in this thread when you start it." |
| 2026-10-23 | Aicent-com | mapping draft v0 prepared (not yet posted) |
| 2026-10-26 | Aicent-com | draft v0 posted in-thread with re-run baseline; v0.1 established here as the canonical version |

## Verification log

| date | check | result |
|---|---|---|
| 2026-10-26 | PyPI `rttp[ed25519]==1.3.1` self-test (clean target dir, Python 3.14.2, win32) | [PASS] 83/83 |
| 2026-10-26 | npm `@aicent/rttp@1.3.1` self-check (node, independent implementation) | [PASS] 35/35 |
| 2026-10-26 | https://iqa.org/sealed-mcp/ live check | seal `iqa://f124b59fc28315c4da79348b37c28a74.forge.iqa` · organ `forge` · standing RADIANT · 22 verdicts · leases until 2026-11-13 |

## Archival note

The pre-canonical draft is archived in the RTTP & IQA project archive as `outreach/draft-2026-10-26-adr163-interchange-mapping-v0.md`; this repository is the canonical home going forward. Substantive revisions are append-only in this table.
