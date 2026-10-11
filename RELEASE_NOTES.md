# Release Notes

## v1.0.4
GH#1011 — add the prompt this skill never had. 14 published steps across 8 packages declared the non-existent `local.transform` step type, which needs no prompt; the engine had no handler, so they fell through to the LLM default with nothing to send and the author saw the model complaining about a prompt nobody wrote. This skill now ships the prompt its consumers bind to.

`target_format` is a step-level `context` binding, not a value baked into the prompt: the skill supports six formats, so a hard-coded one would serve one consumer and force a fork for the next. The format is data about the use, not prose about the capability.

Not mapped to the `format-convert` builtin — it converts JSON pretty/min and HTML to text, and cannot produce a presentation outline from prose.

## v1.0.3
GH#845 — republish with American English (en-US) content, completing the source-only GH#805 flip that never reached the Hub. Copy only — no functional or behaviour change.

## v1.0.2
GH#657 Framing B — republish wave. Bundle now ships `dependencies: []` in its signed manifest (injected by `publish-skrpt.mjs` for `--shared` publishes), so the App's dep-referenced install pipeline (post-PR #47) accepts it on standalone update via Hub Update-all. No content changes.

## v1.0.1
GH#645 Row 3a — republish with `manifest.id` aligned to Hub catalog UUID. Pre-K-037 v1.0.0 bundle carried a local `manifest.id` that drifted from the catalog UUID. Row 5 (`0d9c9dbe`) reconciled the source file but not the signed bundle; v1.0.1 ships the corrected `manifest.id` so the batch-of-81 consumer migrations (GH#645 Row 3b) can pin this version and pass engine STEP 4d. No content changes.

## v1.0.0
Initial catalog release as independent shared object (GH#612 Wave 3).
