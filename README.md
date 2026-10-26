# interchange

Umbrella repository for multi-party interchange work: field mappings, common formats, and cross-scheme compatibility documents, co-drafted with external implementers.

## Principles

- **No party's brand in any name.** The repository and every folder are named after the shared subject, never after either side's product or organization.
- **One folder per collaboration.** A new counterpart or a new topic gets a new folder, not a new repository.
- **Co-drafting implies no joint ownership.** Each side retains sole authority over its own specification; interchange documents bind artifacts, not projects.
- **Everything verifiable.** Stabilized documents are sealed per the IQA release discipline (dual address `rttp://...` / `iqa://...`) and recorded in the release-attestations bundles.

## Folders

| folder | counterpart | status |
|---|---|---|
| [`receipt-interchange/`](receipt-interchange/) | rugsnare (Paraphern) — PIN-SPEC pins vs IQA sealed envelopes | v0.1 draft, co-editing · thread: [uber/ADR#163](https://github.com/uber/ADR/issues/163) |

## Contributing

PRs welcome. Commits must carry `Signed-off-by` (DCO). Discussion lives in each folder's co-drafting thread (see the folder's README).

## License

Apache-2.0
