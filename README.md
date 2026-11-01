# free-claude-skills

21 free Claude skills for everyday professional roles, from [KissMySkills](https://kissmyskills.com). Each skill is a plain `SKILL.md` plus one worked example file. They run offline, need no account, no API key and no server of ours, and are MIT licensed.

Role skills in this repo: travel agent, scriptwriter, ghostwriter, legal assistant, contract reviewer, Wix SEO, controller, accountant, agency account manager, 2D animator, art director, invoice and executive-summary writers, interior design, meal planning, resume screening, job descriptions, Google Ads, software architecture, market research.

## Install

**Claude Code** (all skills as one plugin):

```bash
claude plugin marketplace add Kreal-51/free-claude-skills
claude plugin install kms-free-skills@kissmyskills-free
```

Or inside a session: `/plugin marketplace add Kreal-51/free-claude-skills`, then `/plugin install kms-free-skills@kissmyskills-free`. Skills are then called as `/kms-free-skills:<skill-name>` or picked up automatically when your request matches.

**One skill only, in Claude Code:** copy its folder from `skills/` to `~/.claude/skills/` (all projects) or `.claude/skills/` (one project).

**Claude.ai:** zip the skill folder (the folder itself must be the top level of the zip, for example `marco-travel-agent/SKILL.md`), then open Settings > Features (Capabilities), upload the zip under Skills. Custom skills need a paid plan with code execution enabled.

## Skills

| Skill | Role | What it does |
|---|---|---|
| [`marco-travel-agent`](skills/marco-travel-agent/SKILL.md) | Travel Agent | Senior Travel Agent who knows how the travel industry works and uses that knowledge to help people spend their money better |
| [`ryan-chief-of-staff`](skills/ryan-chief-of-staff/SKILL.md) | Chief of Staff | Senior Chief of Staff with deep experience supporting CEOs, founders, and C-suite executives |
| [`max-scriptwriter`](skills/max-scriptwriter/SKILL.md) | Scriptwriter | Senior Scriptwriter who writes words designed to be spoken, heard, and watched, not read silently |
| [`charlotte-ghostwriter`](skills/charlotte-ghostwriter/SKILL.md) | Ghostwriter | Senior Ghostwriter who writes content published under someone else's name |
| [`victoria-legal-assistant`](skills/victoria-legal-assistant/SKILL.md) | Legal Assistant | Senior Legal Assistant with 10+ years of experience in law firms and in-house legal departments |
| [`marco-contract-reviewer`](skills/marco-contract-reviewer/SKILL.md) | Contract Reviewer | senior contract reviewer |
| [`vix-wix-seo-specialist`](skills/vix-wix-seo-specialist/SKILL.md) | Wix SEO Specialist | Senior Wix SEO Specialist who optimises Wix websites for organic search — from technical setup through to on-page optimisation and content structure |
| [`clara-controller-accountant`](skills/clara-controller-accountant/SKILL.md) | Controller / Accountant | financial controller and accounting specialist |
| [`ai-accountant`](skills/ai-accountant/SKILL.md) | Staff Accountant | Acts as a general staff accountant who handles day-to-day bookkeeping questions, journal entries, account reconciliation logic, and financial statemen |
| [`reese-agency-account-manager`](skills/reese-agency-account-manager/SKILL.md) | Agency Account Manager | Senior Agency Account Manager who writes client status updates, difficult-conversation scripts, and upsell pitches that keep accounts renewing instead |
| [`nikolai-2d-animator`](skills/nikolai-2d-animator/SKILL.md) | 2D Animator | Senior 2D Animator skill |
| [`halbert-art-director`](skills/halbert-art-director/SKILL.md) | Art Director | Senior Art Director skill |
| [`ai-invoice-generator`](skills/ai-invoice-generator/SKILL.md) | Invoice Generator | Turns raw, unstructured billing information - pasted text, a list of services, a quick note about what a client owes - into a complete professional in |
| [`ai-executive-summary-generator`](skills/ai-executive-summary-generator/SKILL.md) | Executive Summary Writer | Condenses a long document, report, plan or raw set of notes into a tight executive summary that gives a busy reader the key facts, decisions and recom |
| [`stella-interior-design`](skills/stella-interior-design/SKILL.md) | Interior Design Advisor | Senior Interior Design Advisor who provides design guidance, colour advice, and styling direction for home interiors |
| [`paolo-meal-planner`](skills/paolo-meal-planner/SKILL.md) | Meal Planner | Senior Meal Planner and Prep Specialist who builds practical, personalised weekly meal plans with integrated shopping lists and batch prep guides |
| [`alex-resume-screener`](skills/alex-resume-screener/SKILL.md) | Resume Screener | Senior Resume Screener and Talent Sourcing Specialist |
| [`ai-job-description-generator`](skills/ai-job-description-generator/SKILL.md) | Job Description Writer | Writes complete, well-structured job descriptions from a short brief about the role, including responsibilities, requirements, and an inclusive tone. |
| [`max-google-ads`](skills/max-google-ads/SKILL.md) | Google Ads Specialist | Activate Max, a Senior Google Ads Specialist, whenever the user needs help with Google Ads or paid search |
| [`julian-software-architect`](skills/julian-software-architect/SKILL.md) | Software Architect | Senior Solution Architect and Software Architect skill |
| [`serena-market-researcher`](skills/serena-market-researcher/SKILL.md) | Market Researcher | Senior Market Researcher who helps businesses, entrepreneurs, and strategists understand their markets through evidence-based analysis |

## Want more?

This repo is a free sample. KissMySkills also sells a larger catalog of paid skills, agents and prompt packs at https://kissmyskills.com. You do not need it to use anything here.

Browse by role:

- Travel Food Home: https://kissmyskills.com/collections/travel-food-home-skills
- Business Consulting Operations: https://kissmyskills.com/collections/business-consulting-operations-skills
- Content Writer: https://kissmyskills.com/collections/content-writer-skills
- Legal Counsel: https://kissmyskills.com/collections/legal-counsel-skills
- Seo Specialist: https://kissmyskills.com/collections/seo-specialist-skills
- Accountant: https://kissmyskills.com/collections/accountant-skills
- Sales Marketing Growth: https://kissmyskills.com/collections/sales-marketing-growth-skills
- Creative Content Design: https://kissmyskills.com/collections/creative-content-design-skills
- Ai Document Generators: https://kissmyskills.com/collections/ai-document-generators
- Ai Recruiter: https://kissmyskills.com/collections/ai-recruiter
- Ai Marketer: https://kissmyskills.com/collections/ai-marketer
- Solutions Architect: https://kissmyskills.com/collections/solutions-architect-skills
- Business Analyst: https://kissmyskills.com/collections/business-analyst-skills

## License

MIT, see [LICENSE](LICENSE). Skills give general guidance, not professional advice: check legal, tax, medical and financial output with a qualified person.
