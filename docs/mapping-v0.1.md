# PIN ↔ Envelope Receipt Interchange — Field Mapping v0.1 (draft for co-editing)

Canonical home of the mapping begun in [uber/ADR#163](https://github.com/uber/ADR/issues/163); see [`PROVENANCE.md`](../PROVENANCE.md) for the comment timeline. Discussion may continue in-thread or here; this file is the authoritative version.

Worth saying up front: the interchange below is also the receipt format the Sensor &rarr; envelope emission sketch (from the original proposal) would emit — if it lands, it becomes a concrete piece of the ADR evidence layer, not a side conversation.

Before the table: we re-ran the step-one verification on our side today, so the baseline starts green from both directions.

### 1. Verified baseline (2026-10-26)

```
pip install "rttp[ed25519]==1.3.1" && python -m rttp.selftest
# [PASS] all 83 checks passed            (clean target dir, re-run 2026-10-26)

npx -y @aicent/rttp@1.3.1
# [PASS] all 35 checks passed (node, independent implementation)
```

The sealed-verdict demo at https://iqa.org/sealed-mcp/ verifies PASS as of today (page seal `iqa://f124b59fc28315c4da79348b37c28a74.forge.iqa`, organ `forge`, standing RADIANT).

### 2. Field-level mapping

Taking the four-row skeleton from the thread and expanding to fields:

| field | rugsnare pin (PIN-SPEC §3.2) | sealed envelope (iqa-mcp) |
|---|---|---|
| attests | which bytes were approved — the exact tool contracts served by version X | a verdict rendered over a session — by whom, when, until when |
| subject | `surfaceHash` over the canonical tool array; the canonicalization policy is itself pinned (§3.1) | content-addressed subject derived from the artifact (SHA-256-based, derivation published, byte-for-byte replayable) |
| signature suite | Ed25519 over the pin store; committed public key in-repo | Ed25519 organ signature — organ = named attesting authority, AID = SHA-256(public key), so the verifier needs only the envelope |
| anchoring | release hashes append-only on-chain (Base mainnet) — an anchor independent of the publisher's repo | no chain anchor: portability *is* the anchoring — the verifier holds the envelope bytes and recomputes |
| freshness | none — deliberately immortal | explicit lease (u64 Unix seconds); expired is fail-closed, never "probably fine" |
| issuer identity | publisher's committed key | named organ (closed set: `forge` / `tss` / `gateway`); verdicts are organ-relative and attributable |
| what it is NOT | not a quality verdict — approval ≠ safety | not an approval lineage — never *which* surface was approved |

### 3. Minimal common interchange — three fields

Agreed on the three fields from the thread, with the third made explicit as a discipline rather than a field that can be absent:

1. **content-addressed subject** — tagged with the canonicalization method that produced it, so a policy change can never masquerade as server drift (the PIN-SPEC §3.1 mirror-image stop, generalized).
2. **signature suite + issuer identity** — suite identifier plus issuer tag; the verifier learns which key material to expect without contacting a directory.
3. **time discipline — an enum, not a default**: `lease { expiry }` | `immortal`. The "no expiry is a property, not an omission" principle (rugsnare, #163) carries as the explicit `immortal` arm, so a verifier never has to guess whether a missing timestamp means "forever" or "broken".

One rule across both systems: a signature-suite or canonicalization bump surfaces as **its own event type**, never as a silent re-interpretation of existing receipts.

### 4. Boundaries — what neither artifact may quietly become

- The pin must not become a verdict: it attests bytes, and stays cheap *because* it refuses to grade them.
- The envelope must not become an approval: it attests a verdict and its lease; the approval step remains human.
- So the audit chain walks three distinct layers — **bytes (pin) / verdict (envelope) / approval (human)** — and the mapping doc should keep them visibly separate rather than let the interchange blur them.

### 5. The chaining story — what the auditor actually gets

An auditor holding both artifacts walks, offline:

> pin: "these exact tool contracts were approved at release X — hash-pinned, chain-anchored"
> ↓
> envelope: "this session was verified against standing S, by organ O, valid until T"

…without contacting either issuer, and without trusting either publisher's repo. Stated honestly: the chain proves **continuity of evidence**, not safety. The judgment stays where you put it — with the human approval step.

### 6. Working plan

- Both sides run §1 independently and post observed results in the #163 thread before the table freezes — the mapping starts from a verified baseline, as proposed in-thread.
- This document carries a version number and lives as a standalone file at this repository; a pointer stays in the #163 thread to keep it lean for the maintainers.
- Co-drafting implies no joint ownership — each side retains sole authority over its own specification; the interchange binds artifacts, not projects.
- Open item for the rugsnare side: whether `immortal` should also carry the chain-anchor reference as part of the interchange (so the "independent of the repo" property travels with the receipt), or stays PIN-SPEC-internal. We take no position yet — it is exactly the kind of non-carried-property question the doc exists to answer.

---
*v0.1 · 2026-10-26 · canonical home: Aicent-Stack/pin-envelope-interchange · co-drafting thread: uber/ADR#163 · RTTP (Resonant Time Transfer Protocol) & IQA (Identity Quality Assurance) sides · canonical forms `rttp://` and `iqa://`*
