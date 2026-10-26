# Preview 30 release evidence

The wrapper payload matches the released Bit Lantern Claude integration. Native release:
`v1.0.0-preview.30`, commit `cf1e0207ca530aa32bfe1273f5f4f2a1758922c3`.

- Released Linux executable SHA-256: `9931347ef4a2d0215e701bd5245a28b0e32a3fb12928a9cb86682e1c1c780dee`.
- Claude Code 2.1.309: strict plugin/marketplace validation passed.
- Live released-runtime probes passed MCP 2026-07-28 and 2025-11-25, with six Free tools,
  complete schemas, correct workspace binding, and clean stdio shutdown.
- One bounded live orientation fixture passed all graders (score 1.00, 24 seconds, $0.15).
  It used indexed navigation and read the referenced source for normalization, lookup,
  expiry, invalidation, and storage.
- Wrapper release tag: `bitlantern--v1.0.0-preview.30`.

The GitHub marketplace is the direct distribution path. Anthropic's directory submission
is tracked separately; this document does not claim directory approval or publication.

On 2026-10-26 the signed GitHub wrapper was pushed at commit
`d26bafe6e64194e3f63d9175748f389c8520fb46`. The existing Anthropic directory update
remains pending: the publication browser had no connected signed-in session, so no Preview 30
portal submission, approval, or publication was observed. Publisher follow-up: update the existing
submission at <https://platform.claude.com/plugins/submit> with this release tag, then record its
actual review state. The direct GitHub marketplace remains usable.
