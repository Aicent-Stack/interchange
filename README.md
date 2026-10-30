# interchange

Umbrella repository for multi-party interchange work: field mappings, common formats, and cross-scheme compatibility documents, co-drafted with external implementers.

The subject matter sits on top of the dual-pillar line — derived intent addressing (`rttp://`) and offline attestation (`iqa://`) — as specified in the combined Individual Submission Internet-Draft [`draft-li-rttp-iqa-addressing`](https://datatracker.ietf.org/doc/draft-li-rttp-iqa-addressing/) (revision -01, 34 pp., 2026-10-27). Interchange documents bind **artifacts and their byte formats**, not implementations and not projects.

## Principles

- **No party's brand in any name.** The repository and every folder are named after the shared subject, never after either side's product or organization.
- **One folder per collaboration.** A new counterpart or a new topic gets a new folder, not a new repository.
- **Co-drafting implies no joint ownership.** Each side retains sole authority over its own specification; interchange documents bind artifacts, not projects.
- **Everything verifiable.** Stabilized documents are sealed per the IQA release discipline (dual address `rttp://...` / `iqa://...`) and recorded in the release-attestations bundles.

## How a collaboration works

1. **Thread first.** A collaboration starts in an existing public thread (an issue, a mailing-list post, a review comment) where both sides' positions are on the record. The folder's README links to that thread; nothing in this repository should be the first place a claim appears.
2. **Co-draft in one folder.** Field mappings and format comparisons are drafted as ordinary Markdown in the counterpart's folder, with both sides' artifacts cited by name and digest — not by marketing page.
3. **Freeze, then seal.** When a document stabilizes, its bytes are frozen and sealed per the IQA release discipline: the seal derives the dual address from the document's own digest (`rttp://<digest>.…` / `iqa://<digest>.…`), so the address is a property of the bytes, not of either party's say-so. Sealed records are appended to the release-attestations bundles ([rttp.com/attestations/](https://rttp.com/attestations/) · [iqa.org/attestations/](https://iqa.org/attestations/)) and resolve through the public resolvers ([rttp.com/open/](https://rttp.com/open/) · [iqa.org/open/](https://iqa.org/open/)).
4. **Append-only afterwards.** A superseded document is marked superseded, pointing at its successor — its seal and its bytes are never rewritten. If a draft changes materially after sealing, that is a new seal on new bytes, with `supersedes` provenance; the old record stays.

## Folders

| folder | counterpart | status |
|---|---|---|
| [`receipt-interchange/`](receipt-interchange/) | rugsnare (Paraphern) — PIN-SPEC pins vs IQA sealed envelopes | v0.1 draft, co-editing · thread: [uber/ADR#163](https://github.com/uber/ADR/issues/163) |

## What this repository is not

- **Not a conformance lab.** Independent runs and sealed run records live in [`conformance`](https://github.com/Aicent-Stack/conformance); this repository holds format-level documents agreed between parties.
- **Not a joint specification.** Neither side's normative text lives here. Each party's scheme remains under its own change control; an interchange document that both sides treat as normative is signed and released by each side separately, cross-referenced here.
- **Not an endorsement feed.** Linking a counterpart's artifact states that it was examined, not that it is approved.

## Contributing

PRs welcome. Commits must carry `Signed-off-by` (DCO). Discussion lives in each folder's co-drafting thread (see the folder's README).

## License

Apache-2.0. Individual interchange documents may credit their co-drafters per folder; those parties retain rights in their own upstream artifacts.
