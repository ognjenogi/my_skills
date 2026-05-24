# Be-Cloud B2B Outreach Brain Generator

## Skill Description
Use this skill whenever the user asks to generate a new batch of outreach emails for Be-Cloud.
Output must be Power Automate-ready Excel/CSV matching the `outreach_brain.xlsx` schema.

---

## 🔴 MANDATORY SKILL MAINTENANCE PROTOCOL

> **Every time something new, important, and verified is discovered during outreach work — this skill MUST be updated immediately and pushed to GitHub.**

This includes (but is not limited to):
- A new **industry hook** that worked or failed
- A new **bad keyword** found in CRM notes that should filter leads
- A new **male name ending in -a** (like Malisa, Vlada) that needs to go in `MALE_NAMES_A`
- A new **format detection edge case** in `parse_row`
- A **column mapping change** in source Excel
- A new **hook** from the Hook Library that becomes active
- Any **tone or wording** improvement proven to increase reply rate
- Any **Power Automate** behavior that affects field format requirements

**Protocol after any discovery:**
```bash
# 1. Update the relevant section in this file
# 2. Run the generation script to verify no regressions
# 3. Push to GitHub:
cd /Users/ognjennikolic/.gemini/antigravity/skills
git add .
git commit -m "Update be-cloud-outreach: [describe what was learned]"
git push origin main
```

**Never leave a verified learning undocumented. The skill is the single source of truth.**

---

## ARCHITECTURE OVERVIEW

```
next_mails.xlsx (raw CRM leads)
        ↓
prepare_outreach_brain.py (personalization engine)
        ↓
outreach_brain.csv (intermediate output)
        ↓
convert_to_excel_table.py (Excel table formatter)
        ↓
outreach_brain.xlsx (upload to OneDrive → Power Automate reads this)
```

---

## REQUIRED OUTPUT COLUMNS (in this exact order)

| Column | Type | Description |
|---|---|---|
| `ID` | Text | **EMPTY** — filled manually by user after generation. |
| `Recipient_Email` | Text | Email address from CRM. Never modify. |
| `First_Name` | Text | First name of contact. |
| `Last_Name` | Text | Last name of contact. |
| `Company` | Text | Company name. Never modify or translate. |
| `Initial_Subject` | Text | Format: `Microsoft licence - {Company}` |
| `Initial_Body` | HTML | Initial personalized email. Use `<br />` tags. |
| `F1_Body` | HTML | Follow-up #1 body. Use `<br />` tags. |
| `F2_Body` | HTML | Follow-up #2 body. Use `<br />` tags. |
| `F3_Body` | HTML | Follow-up #3 / Breakup email. Use `<br />` tags. |
| `Status` | Text | Always starts as `READY`. |
| `Date_Sent` | Text | Empty on generation. Format: `yyyy-MM-dd` when set. |
| `First_Message_ID` | Text | Empty on generation. Set by Power Automate. |
| `Reply_Received` | Text | Always starts as `No`. |

> **CRITICAL:** `Date_Sent` must be stored as TEXT (not Date format) in Excel.
> Power Automate compares it as a string `yyyy-MM-dd`. Excel date serial numbers will break Flow #3.

---

## EMAIL STRUCTURE — MANDATORY (Connor Murray Framework)

Every Initial_Body MUST follow this exact 4-part structure. No exceptions.

### Part 1: Assumptive Opening (Vocative)
```
{salutation} {vocative},
```
Never "Poštovani Milan" — always the correct grammatical vocative form.

### Part 2: Who (Credibility — 1 sentence, factual, no superlatives)
One short factual sentence about Be-Cloud. No "top 50", no "vodeći", no invented numbers.
```
Deo sam tima Be-Cloud, Microsoftovog Tier 1 Cloud partnera koji posluje u 7 zemalja Evrope.
```

### Part 3: Why (Industry-specific pain point)
Connect to their specific industry. Make it feel like you know their world and highlight the upcoming July changes and potential benefits (e.g., Copilot/Power Automate).
Example for IT:
```
IT kompanije poput {comp} su među prvima koje osete promene u Microsoft licenciranju. Microsoft od 1. jula menja cene i licencne modele, ali i otključava nove AI i automatizacijske opcije kroz Copilot i Power Automate koje mogu zameniti eksterne alate koje verovatno trenutno plaćate. Kao Tier 1 partner imamo najnovije informacije o promenama koje će se desiti.
```

### Part 4: Ask (CTA — two specific date/time options)
Use an assumptive CTA format:
```
Hajmo na kratak Teams poziv (30 min), {DATE1} ili {DATE2}, i da vidimo gde najbolje možete da iskoristite te promene.
```
Always two options. Assumptive tone ("Hajmo"). Dates must be updated per batch.

### Signature (fixed)
```
Srdačan pozdrav,
Ognjen Nikolić
Be-Cloud | Microsoft Partner
```

---

## VOCATIVE RULES (MANDATORY — Never skip)

The vocative is the grammatical form of the name used after "Poštovani/Poštovana".
**"Poštovani Milan" is WRONG. It must be "Poštovani Milane".**

### How to form the vocative:

| Name ending | Vocative rule | Example |
|---|---|---|
| Consonant (m) | Add **-e** | Milan → **Milane**, Marko → **Marko** (o stays) |
| Ends in **-o** | Keep as-is | Marko → **Marko**, Branko → **Branko** |
| Ends in **-e** | Keep as-is | Darije → **Darije** |
| Ends in **-a** (female) | Drop **-a** add **-o** | Ana → **Ana** (stays), Jelena → **Jelena** |
| Ends in **-a** (male exception) | Keep as-is | Nikola → **Nikola**, Luka → **Luka** |
| Ends in **-ar** | Drop **-ar** add **-re** | Aleksandar → **Aleksandre**, Petar → **Petre** |
| Ends in **-an** | Drop **-an** add **-ane** | Dragan → **Dragane**, Ivan → **Ivane** |
| Ends in **-en** | Drop **-en** add **-ene** | Sreten → **Sretene** |
| Foreign names / no clear ending | Keep as-is | Harvey → **Harvey**, Jan → **Jan** |

### Gender detection for salutation:
```python
male_names_ending_a = {
    "nikola", "luka", "nemanja", "ilija", "sava", "relja", "andrija", 
    "matija", "kosta", "vanja", "sasa", "mihajlo", "anto", "ante"
}
is_female = first_name.lower().endswith("a") and first_name.lower() not in male_names_ending_a
salutation = "Poštovana" if is_female else "Poštovani"
```

### Vocative function (Python):
```python
def get_vocative(first_name):
    n = first_name.strip()
    nl = n.lower()
    
    # Foreign/invariable names
    foreign_no_change = {
        "harvey", "jan", "edin", "roko", "senko", "jure", "lino", "ivo",
        "anto", "ante", "doni", "andrija", "nikola", "luka", "matija", "vanja",
        "nemanja", "ilija", "sava", "relja", "kosta", "sasa", "mihajlo",
        "darko", "marko", "branko", "ranko", "stanko", "slavko", "zdravko", "vlado"
    }
    if nl in foreign_no_change:
        return n  # no change
    
    # Female names ending in -a: keep as-is
    male_names_ending_a = {
        "nikola", "luka", "nemanja", "ilija", "sava", "relja", "andrija",
        "matija", "kosta", "vanja", "sasa", "mihajlo", "anto", "ante"
    }
    if nl.endswith("a") and nl not in male_names_ending_a:
        return n  # Ana stays Ana, Tatjana stays Tatjana
    
    # -ar → -re
    if nl.endswith("ar"):
        return n[:-2] + "re"  # Aleksandar → Aleksandre
    
    # -an → -ane
    if nl.endswith("an") and not nl.endswith("han"):
        return n + "e"  # Ivan → Ivane, Dragan → Dragane
    
    # -o → keep (Marko, Branko)
    if nl.endswith("o") or nl.endswith("e"):
        return n
    
    # Default: consonant → add -e
    if nl[-1] not in "aeiouáéíóú":
        return n + "e"
    
    return n
```

---

## EMAIL TONE RULES (P2P — Peer to Peer)

| FORBIDDEN | CORRECT |
|---|---|
| "Nadam se da ste dobro" | Direct opening |
| "Top 50 globalno" | "Tier 1 Cloud partner" |
| "15-25% uštede" (invented numbers) | Omit or use verifiable claim |
| "Demonstrativno upoznavanje" | "Kratak Teams poziv" |
| Generic "fragmentisani IT alati" | Industry-specific pain |
| Over-long body (>120 words) | Concise, punchy |
| Em-dash — or en-dash – | Use hyphen - or colon |

**The tone must be:** Expert calling a peer, not a salesperson begging for time.

---

## INDUSTRY HOOK REFERENCE (get_why_section function)

The "WHY" section uses the Connor Murray format. It combines industry awareness with the upcoming event (e.g., July 1st changes).

### 1. IT, Software, SaaS, Fintech
> IT kompanije poput {comp} su među prvima koje osete promene u Microsoft licenciranju. Microsoft od 1. jula menja cene i licencne modele, ali i otključava nove AI i automatizacijske opcije kroz Copilot i Power Automate koje mogu zameniti eksterne alate koje verovatno trenutno plaćate. Kao Tier 1 partner imamo najnovije informacije o promenama koje će se desiti.

### 2. Construction, Architecture, Real Estate
> Građevinske kompanije poput {comp} su među prvima koje osete promene u Microsoft licenciranju, posebno kada su u pitanju terenski timovi. Microsoft od 1. jula menja cene i licencne modele, ali i donosi načine da preko Power Automate platforme automatizujete izveštavanje sa gradilišta koristeći softver koji verovatno već imate. Kao Tier 1 partner imamo najnovije informacije o promenama koje će se desiti.

### 3. Telecoms and General
> Telekomunikacione kompanije poput {comp} su među prvima koje osete promene u Microsoft licenciranju. Microsoft od 1. jula menja cene i licencne modele, ali to je i prilika da pomoću ugrađene AI automatizacije optimizujete kompleksne operativne procese bez plaćanja dodatnih softvera. Kao Tier 1 partner imamo najnovije informacije o promenama koje će se desiti.

---

## EMAIL TEMPLATE STRUCTURE

```
{salutation} {vocative},<br /><br />
Deo sam tima Be-Cloud, Microsoftovog Tier 1 partnera koji posluje u 7 zemalja Evrope.<br /><br />
{why_section}<br /><br />
Hajmo na kratak Teams poziv (30 min), {CTA_DATE1} ili {CTA_DATE2}, i da vidimo gde najbolje možete da iskoristite te promene.<br /><br />
Srdačan pozdrav,<br />Ognjen Nikolić<br />Be-Cloud | Microsoft Partner
```

**Rules:**
- No em-dash (—) or en-dash (–). Use comma or period instead.
- `why_section` = Custom 3-sentence Connor Murray block tailored to their industry.
- CTA: Must use the assumptive "Hajmo na kratak Teams poziv (30 min)..." format.
- Do NOT use specific pricing details like "15-25%". Stick to "menja cene i licencne modele".

---

## HOOK LIBRARY — Choose the most relevant for the current moment

### HOW HOOKS WORK

The hook pattern is always: **[Concrete Microsoft event] + [Tier 1 = we have the info] + [implicit meeting value]**

Never say "vidimo da imate problem". Always: "dešava se promena koja vas pogađa, i mi je znamo."

---

### HOOK 1: Price Increase (active: July 2025)
Use when: Microsoft has a scheduled price increase or licensing cost change.
```
Microsoft od 1. jula menja cene i licencne modele, a kao Tier 1 partner imamo najnovije informacije o promenama koje ce se desiti.
```

### HOOK 2: Licensing Model Change (evergreen)
Use when: Microsoft restructures SKUs, merges plans, or changes per-seat vs per-device rules.
```
Microsoft menja nacin licenciranja za kompanije vase velicine, a kao Tier 1 partner imamo najnovije informacije o tome sta to konkretno znaci za vas budzet.
```

### HOOK 3: New Compliance Requirements (EU/NIS2/GDPR)
Use when: EU regulations (NIS2, AI Act, GDPR updates) create new Microsoft compliance obligations.
```
Nove EU direktive menjaju compliance zahteve za kompanije koje koriste Microsoft cloud alate. Kao Tier 1 partner imamo najnovije informacije o tome sta se konkretno ocekuje i od kada.
```

### HOOK 4: End of Support / Platform Transition
Use when: Windows 10 EOL (Oct 2025), legacy product retirement, forced migration windows.
```
Microsoft gasi podrsku za kljucne platforme koje mnoge kompanije jos koriste. Kao Tier 1 partner imamo najnovije informacije o vremenskim rokovima i opcijama za kompanije vase velicine.
```

### HOOK 5: AI / Copilot rollout
Use when: Microsoft bundles or reprices Copilot, new AI features roll out across M365 plans.
```
Microsoft integrise AI alate u M365 pakete i to menja strukturu i cenu pretplata. Kao Tier 1 partner imamo najnovije informacije o tome koje planove ovo direktno pogadja.
```

### HOOK 6: CSP / Partner Program Change
Use when: Microsoft changes CSP terms, NCE policies, or indirect reseller rules.
```
Microsoft menja uslove za kompanije koje kupuju licence kroz partnere. Kao Tier 1 partner imamo najnovije informacije o tome sta to znaci za budzete i ugovore od sledeceg kvartala.
```

---

**How to pick:** Check the current Microsoft news or partner portal. The hook must refer to something real and time-bound. Generic is worse than specific.

### F1_Body:
```python
f1_body = (
    f"{salutation} {vocative},<br /><br />"
    f"Samo da proverim da ste videli moju prethodnu poruku.<br /><br />"
    f"Da li Vam odgovara {F1_DATE1} ili {F1_DATE2}?<br /><br />"
    f"Srdačan pozdrav,<br />Ognjen Nikolić<br />Be-Cloud | Microsoft Partner"
)
```

### F2_Body:
```python
f2_body = (
    f"{salutation} {vocative},<br /><br />"
    f"Značilo bi mi Vaše mišljenje o ovome kada uhvatite malo vremena.<br /><br />"
    f"Srdačan pozdrav,<br />Ognjen Nikolić<br />Be-Cloud | Microsoft Partner"
)
```

### F3_Body (Breakup):
```python
f3_body = (
    f"{salutation} {vocative},<br /><br />"
    f"Vidim da trenutno nema interesa za Microsoft licencnu analizu u {company}. "
    f"Zatvaramo ovu komunikaciju, ali ako se situacija promeni, slobodno me kontaktirajte. "
    f"Konsultacija je uvek besplatna.<br /><br />"
    f"Srdačan pozdrav,<br />Ognjen Nikolić<br />Be-Cloud | Microsoft Partner"
)
```

---

## LEAD FILTERING RULES

Skip a lead if ANY of these are true:
- `size < 8` employees
- Notes contain: `too small`, `mali`, `premali`, `not use microsoft`, `google`, `not interested`, `ne zanima`
- `email` is empty, `"nan"`, or `"Verified"`
- `first_name` is empty or `"nan"`

---

## DATA INTEGRITY RULES (from EMAIL_GENERATION_RULES.md)

1. **Email address** must be 100% identical to CRM. Never fix or guess domains.
2. **Company name** must never be translated, abbreviated, or "beautified."
3. **Never invent numbers** (e.g., "15-25% savings") without a source.
4. **Subject line** format: `Microsoft licence - {Company}` — max 6 words.
5. **No superlatives** — never "top 50", "vodeći", "broj 1". Use factual: "Tier 1 Cloud partner".
6. If anything is uncertain → skip the lead.

---

## POWER AUTOMATE STATUS VALUES

| Status | Meaning |
|---|---|
| `READY` | Generated, not yet sent by Flow #1 |
| `SENT` | Initial email sent. Flow #3 will follow up. |
| `F1` | Follow-up #1 sent |
| `F2` | Follow-up #2 sent |
| `F3` | Breakup email sent. Sequence complete. |
| `REPLIED` | Lead replied. All automated emails stop immediately. |

---

## FOLLOW-UP SCHEDULE

| Follow-up | Day | Time | Status After Send |
|---|---|---|---|
| Initial | Day 0 | Manual | `SENT` |
| F1 | Day 2+ | 09:00 AM | `F1` |
| F2 | Day 4+ | 09:00 AM | `F2` |
| F3 | Day 7+ | 09:00 AM | `F3` |

---

## COLUMN FORMAT IN EXCEL

```
A: ID (empty — user fills manually)
B: Recipient_Email
C: First_Name
D: Last_Name
E: Company
F: Initial_Subject
G: Initial_Body (HTML, <br /> tags)
H: F1_Body (HTML)
I: F2_Body (HTML)
J: F3_Body (HTML)
K: Status = "READY"
L: Date_Sent = "" (TEXT format, not Date)
M: First_Message_ID = ""
N: Reply_Received = "No"
```

---

## FILE PATHS

| File | Path |
|---|---|
| Raw leads | `/Users/ognjennikolic/Documents/be-cloud selling/send/next_mails.xlsx` |
| Generation script | `/Users/ognjennikolic/Documents/be-cloud selling/prepare_outreach_brain.py` |
| Excel converter | `/Users/ognjennikolic/Documents/be-cloud selling/convert_to_excel_table.py` |
| Output CSV | `/Users/ognjennikolic/Documents/be-cloud selling/send/outreach_brain.csv` |
| Output Excel | `/Users/ognjennikolic/Documents/be-cloud selling/send/outreach_brain.xlsx` |
| OneDrive path | `/Attachments/outreach_brain.xlsx` |
| Email rules | `/Users/ognjennikolic/Documents/be-cloud selling/EMAIL_GENERATION_RULES.md` |
