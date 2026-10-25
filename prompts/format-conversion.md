---
type: prompt
id: format-conversion
title: "Format Conversion"
description: "Converts content into a target output format, preserving meaning and organisation"
tags: [Production, Quality]
context_params:
  source_content:
    label: "Source content"
    description: "The content to convert. Any format."
    required: true
  target_format:
    label: "Target format"
    description: "One of: markdown, plain text, email HTML, JSON, CSV, presentation outline. Declared per step — this skill supports all six, so the format belongs to the use, not to the prompt."
metadata:
  output_format: markdown
  prompt_type: task
---

## Purpose

Drives the format-conversion skill (GH#1011).

`target_format` is a step-level `context` binding rather than a value baked in
here. The skill documents six supported formats; a prompt with one hard-coded
would serve one of them, and the first consumer wanting another would have to
fork it — a shared skill acquiring a per-consumer variant, which is the opposite
of why it is shared. The format is data about this use, not prose about the
capability.

## Prompt

You are a formatting specialist. Convert the content below into the target format.

Preserve the source content's meaning and organisation exactly. Do not add, remove, summarise or rewrite the substance — change only how it is presented.

### Source content

{{step.context.source_content}}

### Target format

{{step.context.target_format}}

Follow that format's conventions:

- **markdown** — CommonMark: headings, lists, tables, code blocks, emphasis
- **plain text** — no markup; preserve structure with whitespace and indentation
- **email HTML** — inline-styled HTML, tables for layout, no external stylesheets
- **JSON** — extract fields, arrays and nested objects from the content
- **CSV** — headers from context, one row per record
- **presentation outline** — slide by slide: title, bullet points, speaker notes

Output only the converted content.

## What this does NOT do

- **Choose the target format.** That is the step's `context.target_format`.
- **Alter substance.** No summarising, editing or restructuring beyond the format change.
- **Validate that the content suits the format.** Asking for CSV from prose yields a
  best-effort table. The skill's documentation does not say what should happen
  instead, so this prompt does not invent a rule — the ambiguity is named rather
  than resolved. If a consumer needs strict behaviour there, it belongs in that
  consumer's step, not here.
