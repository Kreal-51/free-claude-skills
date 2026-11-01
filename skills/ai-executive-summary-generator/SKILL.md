---
name: ai-executive-summary-generator
description: "Condenses a long document, report, plan or raw set of notes into a tight executive summary that gives a busy reader the key facts, decisions and recommendations in under a page without reading the source. Use when someone has a business plan that needs a one-page summary for investors, a quarterly report that needs a board summary, or project notes that must become an executive status update, and says \"executive summary\", \"summarize this for leadership\", \"one-pager for the board\", \"TL;DR of this report\" or \"brief the exec team on this\"."
---

# AI Executive Summary Generator

## What this skill does

This skill condenses a longer document, report, plan, or raw set of notes into a tight executive summary that gives a busy reader the key facts, decisions, and recommendations in under a page, without requiring them to read the source material.

## When to use this skill

Use this skill when the user provides a longer piece of content (a business plan, report, meeting notes, project update, research findings) and wants a condensed summary for leadership or stakeholders, including:
- A business plan that needs a one page summary for investors
- A quarterly report that needs a summary for the board
- Project notes that need to become a status update for executives

## Step by step process

1. Read the full source material and identify the core purpose: what is this document about, and what does the reader need to know or decide.
2. Extract the key facts: what happened, what is being proposed, what the current status is, and any numbers that matter (revenue, growth, costs, timeline, risk).
3. Identify any explicit recommendation, ask, or decision point in the source material. If the source does not state one clearly, do not invent one. Instead state the situation neutrally and note that no specific recommendation was included in the source material.
4. Strip out supporting detail, background explanation, and process description that a decision maker does not need to see. This skill's core value is what to cut, not just what to condense.
5. Preserve any hard numbers, dates, and named risks exactly as stated in the source. Do not round, generalize, or approximate figures that were given precisely.
6. If the source material is missing context an executive summary conventionally needs (what the ask is, what the timeline is, what the cost is), note this as a gap rather than filling it with a guess.
7. Keep the summary to roughly one fifth the length of the source material or shorter, and never longer than one page regardless of source length.

## Output structure

Produce the executive summary with these sections in order:
1. Title matching the source document's subject
2. Overview (two to three sentences stating what this is and why it matters right now)
3. Key Points (three to six bullet points covering the most decision relevant facts, each one line)
4. Numbers That Matter (any critical figures, only if present in the source)
5. Recommendation or Ask (stated only if the source contained one, otherwise noted as not specified)
6. Risks or Open Questions (if mentioned in the source)

## Tone and formatting guidance

Write in short, declarative sentences. Every sentence should carry information a decision maker needs, not context they already have or filler transitions. Avoid hedging language ("it seems," "possibly," "may potentially") unless the source material itself was uncertain, in which case preserve that uncertainty accurately rather than smoothing it into false confidence. Do not add opinions, forecasts, or recommendations that are not grounded in the source material, since an executive summary is meant to compress facts accurately, not to add new analysis.

---

Free edition from [KissMySkills](https://kissmyskills.com), released under the MIT license as part of [free-claude-skills](https://github.com/Kreal-51/free-claude-skills). More skills for this role: https://kissmyskills.com/collections/ai-document-generators
