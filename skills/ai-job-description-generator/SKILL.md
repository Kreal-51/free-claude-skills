---
name: ai-job-description-generator
description: Writes complete, well-structured job descriptions from a short brief about the role, including responsibilities, requirements, and an inclusive tone.
---

# AI Job Description Generator

## Purpose

This skill turns a short brief (job title, a few bullet points, or a rough description) into a complete, professional job description ready to post. It produces consistent sections every time and avoids biased or exclusionary language.

## When to use this skill

Use this skill when the user asks to write, draft, or improve a job description, job posting, or job ad. Trigger phrases include "write a job description for", "draft a JD for", "I need a posting for a [role]", or "help me write a job ad".

## Instructions

1. Start by identifying what the user has already told you: job title, seniority level, department, key responsibilities, must-have skills, and company or team context. Ask only if something critical is missing and cannot be reasonably inferred (for example, if no seniority level is given, default to writing for a mid-level version of the role and say so).
2. Write in a professional but approachable tone. Avoid corporate jargon like "rockstar", "ninja", "wear many hats", or "fast-paced environment" unless the user explicitly asks for that style.
3. Use inclusive language throughout. Avoid gendered phrasing, avoid unnecessary requirements that filter out qualified candidates (like requiring a specific degree when equivalent experience should count), and avoid superlatives that discourage otherwise-qualified applicants from applying ("must be an expert in everything listed").
4. Separate "required" qualifications from "nice to have" qualifications. Keep the required list short and genuinely essential; move anything soft or aspirational to nice to have.
5. Include a brief, honest role summary at the top that explains why the role exists and what success looks like, not just a list of duties.
6. Do not invent compensation, benefits, or company details that were not provided. Leave a clear placeholder like "[Add compensation range]" or "[Add benefits summary]" rather than making something up.
7. Keep responsibilities action-oriented (start with verbs: "Own", "Lead", "Build", "Partner with") rather than vague noun phrases.

## Output format

```
# [Job Title]
[Department/Team] | [Location or Remote] | [Employment Type]

## About the Role
[2-3 sentences on why this role exists and what success looks like]

## What You'll Do
- [Responsibility]
- [Responsibility]

## What We're Looking For
Required:
- [Requirement]

Nice to Have:
- [Requirement]

## Compensation & Benefits
[Add compensation range]
[Add benefits summary]
```

## Edge cases

- If the user gives only a job title with no other detail, generate a reasonable draft based on how that role is typically defined, but flag clearly at the top: "Draft based on typical expectations for this role  -  please review and adjust for your specific needs."
- If the brief conflicts with itself (for example, calling for a senior title but listing entry-level responsibilities), point out the mismatch rather than silently picking one.
- If the role is niche or highly technical, keep required qualifications specific and verifiable rather than generic ("5+ years of X" only if the user actually wants a hard requirement).

## Compatibility

This skill produces identical structured output in Claude and ChatGPT. Provide the role brief in the chat and ask for a job description; no special setup is needed.

---

Free edition from [KissMySkills](https://kissmyskills.com), released under the MIT license as part of [free-claude-skills](https://github.com/Kreal-51/free-claude-skills). More skills for this role: https://kissmyskills.com/collections/ai-recruiter
