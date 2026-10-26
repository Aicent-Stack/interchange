# pin-envelope-interchange

Field-level mapping between **rugsnare pins** (PIN-SPEC §3.2, release-time approval attestation) and **IQA sealed envelopes** (iqa-mcp, runtime verdict attestation), working toward a minimal common interchange for receipt formats.

## Status

- **Current version:** v0.1 — draft for co-editing
- **Co-drafting thread:** [uber/ADR#163](https://github.com/uber/ADR/issues/163) (discussion) · this repository (canonical versioning, PRs welcome)
- **Principle:** co-drafting implies no joint ownership — each side retains sole authority over its own specification; the interchange binds artifacts, not projects.

## Documents

- [`docs/mapping-v0.1.md`](docs/mapping-v0.1.md) — field mapping, verified baseline, minimal interchange proposal, boundaries, chaining story, working plan.

## Provenance

- [`PROVENANCE.md`](PROVENANCE.md) — the #163 comment timeline this draft descends from, and the verification log.

## Verification

Everything on the IQA side is offline-verifiable today:

```
pip install "rttp[ed25519]==1.3.1" && python -m rttp.selftest   # [PASS] 83/83
npx -y @aicent/rttp@1.3.1                                        # [PASS] 35/35
```

Once the field table stabilizes, each version of the mapping document will be sealed per the IQA release discipline (dual address `rttp://…` / `iqa://…`) and recorded in the release-attestations bundles.

## Contributing

PRs welcome. Commits must carry `Signed-off-by` (DCO). Discussion may continue either in the #163 thread or here via issues — this file tree is the authoritative version.

## License

Apache-2.0
