# Be-Cloud B2B Outreach Brain Generator

## Skill Description
Use this skill whenever the user asks to generate a new batch of outreach emails for the Serbian B2B market. This skill documents the exact pipeline from raw lead data to a Power Automate-ready Excel "Brain."

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

## REQUIRED OUTPUT COLUMNS

The generated CSV/Excel MUST have exactly these columns in this order:

| Column | Type | Description |
|---|---|---|
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
> Power Automate compares it as a string `yyyy-MM-dd`. Excel's date serial numbers (e.g. `46152`) will break the date comparison filter in Flow #3.

---

## EMAIL BODY FORMATTING RULES

### MANDATORY: Use HTML `<br />` tags (not newlines)
Power Automate sends email bodies as HTML. Plain newlines `\n` are ignored by Outlook.

**Correct:**
```python
f"{salutation} {first_name},<br /><br />Deo sam tima Be-Cloud..."
```

**Wrong:**
```python
f"{salutation} {first_name},\n\nDeo sam tima Be-Cloud..."
```

### Never use em dash (—) or en dash (–)
These break rendering in some email clients. Use a regular hyphen (-) or colon instead.

### Max 120 words per email body.

### CTA must include two specific date/time options
Example: `sreda (13. maj) u 10h ili četvrtak (14. maj) u 14h`
Update dates for each new batch before generating.

---

## FOLLOW-UP SCHEDULE

| Follow-up | Day | Time | Status After Send |
|---|---|---|---|
| Initial | Day 0 | Manual | `SENT` |
| F1 | Day 2+ | 09:00 AM | `F1` |
| F2 | Day 4+ | 09:00 AM | `F2` |
| F3 | Day 7+ | 09:00 AM | `F3` |

Power Automate Flow #3 checks: `Date_Sent < today - 2 days` before sending each follow-up.

---

## GENDER / SALUTATION LOGIC

```python
male_names_ending_in_a = {"nikola", "luka", "nemanja", "ilija", "sava", "relja", 
                           "andrija", "matija", "kosta", "vanja", "sasa", "mihajlo"}

is_female = first_name.lower().endswith("a") and first_name.lower() not in male_names_ending_in_a
salutation = "Poštovana" if is_female else "Poštovani"
```

---

## INDUSTRY HOOK LOGIC

Each industry maps to three Serbian-language values:
1. `ind_serbian` — how we describe the industry segment
2. `problem` — the specific pain point
3. `loss` — the business consequence

Used in Initial_Body template:
```
Kroz rad sa {ind_serbian} kompanijama često viđamo da se bore sa {problem}.
Ovaj problem obično predstavlja najveći {loss} u IT-ju.
```

Refer to `get_industry_hook()` function in `prepare_outreach_brain.py` for the full mapping.

---

## LEAD FILTERING RULES

Skip a lead if ANY of these are true:
- `size < 8` employees
- Notes contain: `too small`, `mali`, `premali`, `not use microsoft`, `google`, `not interested`, `ne zanima`
- `first_name` is empty or `"nan"`

---

## DATA INTEGRITY RULES (from EMAIL_GENERATION_RULES.md)

1. **Email address** must be 100% identical to CRM. Never fix or guess domains.
2. **Company name** must never be translated, abbreviated, or "beautified."
3. **Never invent numbers** (e.g., "15-25% savings") without a source.
4. **Subject line** max 6 words. Never use "revizija" or "optimizacija".
5. If anything is uncertain → add `// UNSURE` and skip the lead.

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

## STEP-BY-STEP: GENERATING A NEW BATCH

### Step 1: Prepare the raw leads file
- Export new leads from CRM into: `send/next_mails.xlsx`
- Verify: no duplicates, correct emails, company names intact.

### Step 2: Update dates in the script
Open `prepare_outreach_brain.py` and update:
```python
suggested_date_1 = "utorak (X. mesec) u 10h"
suggested_date_2 = "sreda (X. mesec) u 14h"
```
And in `initial_body`, update the CTA dates:
```python
"Da li Vam više odgovara sreda (X. mesec) u 10h ili četvrtak (X. mesec) u 14h..."
```

### Step 3: Run the generation script
```bash
python3 "/Users/ognjennikolic/Documents/be-cloud selling/prepare_outreach_brain.py"
```
Output: `send/outreach_brain.csv`

### Step 4: Convert to Excel with proper Table structure
```bash
python3 "/Users/ognjennikolic/Documents/be-cloud selling/convert_to_excel_table.py"
```
Output: `send/outreach_brain.xlsx` with `OutreachTable` inside.

### Step 5: Fix Date_Sent column format in Excel
- Open `outreach_brain.xlsx`
- Select the `Date_Sent` column
- Format Cells → **Text** (NOT Date)
- Save and close.

### Step 6: Upload to OneDrive
- Upload `outreach_brain.xlsx` to the `/Attachments/` folder in OneDrive.
- Replace the previous file.
- Power Automate will automatically read the new leads.

---

## POWER AUTOMATE FLOWS OVERVIEW

### Flow #1: Initial Sender
- **Trigger:** Manual
- **Filter:** `Status eq 'READY'`
- **Action:** Send email (V2) with `Initial_Subject` and `Initial_Body`
- **Importance:** Normal (always set explicitly)
- **Delay:** 1-2 minutes between each send (prevents domain ban)
- **Update:** Status → `SENT`, Date_Sent → `utcNow()` formatted as `yyyy-MM-dd`

### Flow #2: Reply Tracer
- **Trigger:** When a new email arrives (Outlook)
- **Filter Query:** `Recipient_Email eq '{From}'` (no spaces around the email)
- **Action:** Update row → `Reply_Received` = `Yes`, `Status` = `REPLIED`

### Flow #3: Follow-up Engine
- **Trigger:** Recurrence — every day at 09:00 AM
- **Filter:** `Reply_Received eq 'No'`
- **Condition:** `Date_Sent` ≤ `formatDateTime(addDays(utcNow(), -2), 'yyyy-MM-dd')`
- **Switch on Status:**
  - `SENT` → Send F1, update Status=`F1`, Date_Sent=today
  - `F1` → Send F2, update Status=`F2`, Date_Sent=today
  - `F2` → Send F3, update Status=`F3`, Date_Sent=today
- **Email Body format:** Follow-up body + separator + previous bodies (quoted thread)
- **Subject format:** `Re: {Initial_Subject}`

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
| CRM reference | `/Users/ognjennikolic/Documents/be-cloud selling/Ognjen_Serbia_17_03_2026_enriched_with_notes.xlsx` |
| Email rules | `/Users/ognjennikolic/Documents/be-cloud selling/EMAIL_GENERATION_RULES.md` |
