---
name: discovery-call-prep
description: Use when the user asks to prepare for a Discovery Call, research a company before a meeting, generate a Point of View (POV) slide, or create a customized Credibility Statement based on the Connor Murray OEA framework.
---

# Discovery Call Preparation Skill (Salesmotion 2026)

## Overview
This skill is designed to fully prepare the user for a Discovery Call using the Connor Murray methodologies. It automates company research, identifies industry-specific pain points, and generates the exact scripts (Credibility Statement and POV) needed to establish authority immediately.

## Step 1: Deep Company Research
When the user provides a company name or website, you must actively research them (using web search tools if available) or use your knowledge to gather:
1. **Industry & Business Model:** What exactly do they do? How do they make money?
2. **Recent News & Public Goals:** Have they recently acquired a company, expanded, laid off staff, or announced new strategic goals?
3. **Tech Stack & Operations (if applicable):** What kind of departments or processes are core to their business?

## Step 2: The POV (Point of View) Strategy
Generate the talking points for the "Point of View" slide (used especially for C-Level executives). This should be 3 bullet points:
1. **Javni ciljevi (Public Goals):** What the company is publicly trying to achieve right now (based on Step 1).
2. **Prioriteti (Priorities):** What the specific executive's department is likely focusing on to support those goals.
3. **Vaša pretpostavka (The Assumption):** A highly educated guess about the biggest problem holding them back (which the user's product solves).

## Step 3: The Credibility Statement
Generate a customized Credibility Statement based on the objective template. Fill in the placeholders with the specific industry data you gathered. You must assume the user's role/company if known from context, or use placeholders.

**Format (Translate filled placeholders to Serbian):**
> *"Sjajno, da počnemo. [Tvoje Ime] ovde, u [Tvoja Kompanija] sam i deo sam tima koji radi prevashodno sa [Njihova Industrija] kompanijama.*
> *Obično nas [Ciljno Odeljenje klijenta] angažuju kada prolaze kroz [Glavni proces klijenta/Tranziciju]. Najčešće rešavamo probleme oko [Problem 1], [Problem 2] i [Problem 3].*
> *Naš ishod je obično [Krajnji Benefit 1] i [Krajnji Benefit 2] bez probijanja budžeta.*
> *Znam da je ovo onako 'high-level', pa me zanimalo da li vam išta od ovoga zvuči poznato? Voleo bih da čujem od Vas – šta je vaš trenutni primarni fokus za ovu godinu, pa možemo odatle?"*

## Step 4: Industry-Specific Question Funnels (Pain Points)
Provide the user with the 3 most common pain points for this specific industry/company type. For each pain point, provide 2 "Exploration" questions (T.E.D. technique - Tell, Explain, Describe) the user can ask to get the prospect talking.

**Example for a Pain Point:**
- **Problem:** Manuelna alokacija resursa.
- **T.E.D. Pitanje 1:** *"Možete li mi opisati kako tačno izgleda vaš proces kada novi zaposleni dođe u firmu?"*
- **T.E.D. Pitanje 2:** *"Pomozi mi da razumem – koliko vremena vaš tim trenutno gubi na administriranje licenci svakog meseca?"*

## Output Format
Your response MUST be structured exactly like this:
1. 🏢 **Company & Industry Brief:** (Short summary of what they do and their current goals).
2. 🎯 **POV Slajd (Za deljenje ekrana):** (The 3 bullet points).
3. 📜 **Credibility Statement (Skripta):** (The fully customized intro).
4. 🕵️ **Najčešći Problemi i T.E.D. Pitanja:** (3 industry-specific problems with 2 open-ended exploration questions each).

## Strict Rules
- **Language:** Serbian (Full diacritics: š, đ, č, ć, ž).
- **Tone:** Peer-to-peer consulting. You are preparing an expert, so do not sound like a generic customer service rep.
- Do NOT make the output too long. Keep it actionable and punchy so the user can read it 5 minutes before the call.
