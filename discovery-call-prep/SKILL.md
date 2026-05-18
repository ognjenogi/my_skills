---
name: discovery-call-prep
description: Use when preparing for a P1 discovery call, generating a discovery call script, building signal-based value drops for Microsoft products, synthesizing Microsoft news into P1 sales arguments, or updating the master discovery script with new weekly intel for Be-Cloud prospects.
---

# Discovery Call Prep Skill (Be-Cloud P1)

## Overview

Generates complete P1 discovery call preparation materials by synthesizing the Connor Murray OEA framework, Be-Cloud qualification methodology, Microsoft B2B terminology, and current Microsoft news intelligence into signal-based value arguments.

**Core principle:** Every discovery call must leave the prospect with at least one new insight they didn't have before. The call sells the next step (P2 demo), not the product.

## When to Use

- User says "pripremi discovery call za [prospect]"
- User says "napravi P1 skriptu" or "prepare P1"
- User wants to update the master script with new Microsoft news
- User provides new Microsoft news PDFs/articles for sales intel extraction
- User asks to generate value drops, pain triggers, or objection handles

## Required Reference Files

Before generating ANY output, read these files in order:

1. **Framework:** `/Users/ognjennikolic/Documents/be-cloud selling/strategy/Connor_Murray_Discovery_Call_Strategy.md`
2. **Qualification Questions:** `/Users/ognjennikolic/Documents/be-cloud selling/strategy/P1 Qualification - 16 Questions (Serbian).md`
3. **Master Script:** `/Users/ognjennikolic/Documents/be-cloud selling/strategy/Discovery_Call_Ultimate_Script_v3.md`
4. **Terminology:** `/Users/ognjennikolic/Documents/be-cloud selling/strategy/Microsoft_B2B_Terminology_Guide.md`
5. **News Intel:** All PDFs and MDs in `/Users/ognjennikolic/Documents/be-cloud selling/News/` (use PyMuPDF for PDFs)

---

## Output Type 1: Prospect-Specific P1 Prep

When user provides a specific company/prospect, generate:

### A. Company Brief (3-5 bullets)
- Industry + size + locations
- Known Microsoft stack (if available from CRM)
- Predicted pain points based on industry
- Relevant Microsoft news hooks for their sector
- Decision-maker identification

### B. Customized Credibility Statement (90 seconds)
Adapt the template for their industry:
```
"Sjajno, da krenemo. Ja sam Ognjen iz Be-Cloud-a — mi smo jedan od 
najvećih Microsoftovih partnera za mala i srednja preduzeća...

Obično nas angažuju [THEIR INDUSTRY TYPE] kompanije od [THEIR SIZE RANGE] 
zaposlenih, najčešće kada prolaze kroz [RELEVANT PROCESS]...

Tri najčešća problema zbog kojih nas zovu su:
1. [INDUSTRY-SPECIFIC PAIN 1]
2. [INDUSTRY-SPECIFIC PAIN 2]  
3. [INDUSTRY-SPECIFIC PAIN 3]"
```

### C. TED Question Funnel (5-7 questions)
Industry-specific questions using Tell/Explain/Describe technique:

| Question | TED Follow-up | Signal to Listen For |
|----------|---------------|----------------------|
| [Specific question] | [Deeper probe] | [Green/Red flag] |

### D. Value Drops (3-5, signal-based)
Format each as:

```
**Signal:** "[What the prospect might say]"
> **Value Drop:** "[Specific Microsoft capability + why it matters]"
```

### E. P1→P2 Pivot Script
Customized closing referencing their specific pains and July 1 deadline.

---

## Output Type 2: Master Script Update

When user provides new Microsoft news, extract and integrate:

### Extraction Protocol
For each news item, generate all 5 components:

| Component | Purpose | Language |
|-----------|---------|----------|
| 🎯 Cold Call Hook | Book the P1 | Serbian |
| 🌱 P1 In-Meeting Seed | Open the pain | Serbian |
| ❓ Top Objection Handle | Neutralize resistance | Serbian |
| 🎁 Value Drop | Signal-based argument | Serbian |
| 🔁 P1→P2 Pivot | Close into demo | French |

### Categorization (4 Pillars)
1. **Licensing & Pricing** — Budget urgency, renewal traps, price changes
2. **AI & Copilot** — Copilot features, Shadow IT, agentic capabilities
3. **Cybersecurity** — Defender, Purview, Entra ID, Zero Trust
4. **Power Platform** — Power Automate, Power Apps, Power BI, governance

### Urgency Scoring (1-5)
- **5/5:** Immediate financial/security impact, time-bound
- **4/5:** Strong business case, clear ROI argument
- **3/5:** Good context, supports broader conversation
- **2/5:** Niche, useful only for specific industries
- **1/5:** Background only, no direct sales hook

### Integration Rules
- Items scored 4-5 → Add to Master Script Value Drops
- Items scored 3 → Add to Master Script Rečnik Rešenja table
- Items scored 1-2 → Document in News folder only

---

## Output Type 3: Weekly Intel Brief

When user says "napravi weekly brief" or provides new news sources:

```markdown
# Be-Cloud SMB Microsoft News Briefing
**Date:** [date] | **Target:** SMBs 10-200 employees

## [Pillar Name]
### [News Item Title]
📰 The News: [factual summary]
💡 Why SMBs Care: [business impact]
🔥 Urgency Score: X/5
🎯 Cold Call Hook: [Serbian]
🌱 P1 In-Meeting Seed: [Serbian]
❓ Top Objection Handle: [Serbian]
🔁 P1→P2 Pivot: [French]

## 🎯 Master P1→P2 Closing Script (FR)
[Universal French closing + Fallback line]
```

---

## Strict Rules

### Language
- Questions, hooks, seeds, objection handles → **Serbian** (š, đ, č, ć, ž)
- P1→P2 Pivot scripts → **French** (Be-Cloud internal closing language)
- Code, file names, technical terms → **English**

### Tone — Peer-to-Peer Consultant

| FORBIDDEN | CORRECT |
|-----------|---------|
| "Nadam se da ste dobro" | Direct opening |
| "Top 50 globalno" | "Tier 1 Cloud partner" |
| "15-25% uštede" (invented) | Omit or use verifiable claim |
| "Da li imate minut?" | Assumptive formality |
| Generic "fragmentisani IT alati" | Industry-specific pain |
| Explaining features first | Asking about their pain first |
| Doing a demo on P1 | Selling the P2 demo |

### OEA Framework Compliance
Every output must follow Connor Murray's structure:

1. **Orientation (0-5 min):** Credibility Statement → Open-ended monolog trigger
2. **Exploration (5-25 min):** Question funnels with TED → Signal-based Value Drops
3. **Advancement (25-30 min):** Pain summary → Licensing urgency → Multi-thread → Book P2 on call

### Value Drop Rules
- **Never demo on P1.** Only drop enough that they say "I'd like to see that."
- **Always signal-based.** Listen first, then drop the relevant argument.
- **One insight minimum.** Prospect leaves without learning something = failed call.
- **Concrete > Abstract.** "Copilot reads scanned PDFs" beats "AI improves productivity."
- **Dormant features = strongest argument.** Features they already pay for but don't use.

### Active Licensing Hooks (Update Monthly)

| Hook | Deadline | Impact |
|------|----------|--------|
| Business Basic $6→$7, Standard $12.50→$14 | July 1, 2026 | All SMBs |
| CSP extended service term enforcement | May 4, 2026 | Partners/renewals |
| M365 E7 + Agent 365 GA | May 1, 2026 | Enterprise context |
| Copilot 3-year CSP option | May 13, 2026 | Budget planning |
| Business suite packaging (+50GB mail, URL protection) | June-Aug 2026 | All Business plans |

### Multi-threading Rule
Always push for second stakeholder on P2:
> "Naša politika: ne odobravamo Senior Cloud inženjera ukoliko na pozivu 
> nemamo nekoga ko poznaje i poslovni i tehnički ugao problema."

### Dormant Features Pattern (Strongest Sales Argument)
- Defender Attack Disruption → "spava u Business Premium"
- Teams Brand Impersonation → "mora da se konfigurira"
- Purview DLP → "već plaćate, ne koristite"
- SharePoint AI Workflows → "besplatno na pravom planu"
- Copilot Enterprise Data Protection → "podaci nikad ne izlaze iz tenant-a"

---

## PDF Reading Protocol

```python
import fitz  # PyMuPDF — install: pip3 install PyMuPDF
doc = fitz.open(pdf_path)
for page in doc:
    text = page.get_text()
```

⚠️ Excalidraw files (.excalidraw, .excalidraw.md) are binary — skip them.

---

## File Paths

| File | Path |
|------|------|
| Master Script v3 | `strategy/Discovery_Call_Ultimate_Script_v3.md` |
| Connor Murray OEA | `strategy/Connor_Murray_Discovery_Call_Strategy.md` |
| P1 Qualification | `strategy/P1 Qualification - 16 Questions (Serbian).md` |
| B2B Terminology | `strategy/Microsoft_B2B_Terminology_Guide.md` |
| News Folder | `News/` (all subfolders) |
| Cold Call Script | `strategy/Connor_Murray_Cold_Call_Strategy.md` |
| Qualif Sofiane | `strategy/Qualif Sofiane (Serbian Market).md` |

> All paths relative to `/Users/ognjennikolic/Documents/be-cloud selling/`

---

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Turning P1 into a demo | Only drop value hints — sell the P2 |
| "Kakav je vaš proces?" | Specific: "Kako pratite licence bivših zaposlenih?" |
| Inventing savings numbers | Never "15-25% uštede" without source |
| Skipping licensing urgency | Every call mentions July 1 deadline |
| "Javim se mejlom" | Open calendars ON the call |
| Generic Credibility Statement | Customize for their industry |
| French pivot without pain reference | Always reference 2-3 pains they shared |
| Value drops without signals | Listen first, then drop — never lecture |
| Ignoring dormant features | "Already paying, not using" = strongest argument |

---

## Related Skills

- **REQUIRED:** `cold-call-personalization` — For cold call scripts (pre-P1)
- **REQUIRED:** `be-cloud-outreach` — For email outreach generation
- **REFERENCE:** `sales-automator` — For general sales patterns
