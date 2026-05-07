---
name: cold-call-personalization
description: Use when the user asks to generate a personalized cold call script, prepare for a cold call, or research a prospect to find relevant pain points for a call script. This skill enforces the Connor Murray "Who, Why, What" cold call framework for the Serbian market.
---

# Cold Call Personalization Skill (Salesmotion 2026)

## Overview
This skill is designed to generate highly personalized, high-converting cold call scripts based on the Connor Murray "Who, Why, What" framework. It is specifically tailored for the Serbian B2B market, representing Be-Cloud (a Top 50 Global Microsoft Partner).

## Step 1: Research & Info Gathering
When the user provides a lead (or asks you to prepare a script for a lead), you must first identify:
1. **Industry (Industrija):** What does the company do?
2. **Position (Titula):** What is the lead's role? (e.g., IT Manager, CFO, CEO)
3. **Pain Point (Problem):** Based on their industry and role, what is their most likely Microsoft/IT pain point? 
   - *Example (IT/SysAdmin):* Unused licenses, Entra ID chaos, SKU mismatch.
   - *Example (Finance/CEO):* Overpaying for licenses, budget optimization, compliance.
   - *Example (Manufacturing/Logistics):* Frontline worker vs Office worker licenses, field data connectivity.

*If the user doesn't provide enough information, use your web search or knowledge to fill in the gaps before generating the script.*

## Step 2: The Script Generation
Generate the script in **Serbian**. The script MUST follow this exact structure, with NO extra fluff ("Nadam se da ste dobro", "Da li imate minut", etc.).

### A. Assumptive Formality
Always start with:
`Dobar dan [Ime], ovde Ognjen Nikolić iz Be-Clouda, kako ste?`
*(Wait for "Dobro, recite" or similar, then immediately proceed)*

### B. The Value Statement (Who, Why)
Combine the WHO and the WHY in two flowing sentences.

**Who:** `Zovem Vas jer sam ja deo [Specifičan tim, npr. tima za cloud infrastrukturu / tima za poslovna rešenja]...`
**Why:** `...koja najviše sarađuje sa [Njegova Industrija] organizacijama. Najčešće radimo sa timovima kako bismo im pomogli oko [Specifičan Pain Point iz Koraka 1].`

### C. The Ask (What) - Provide 3 Variations
You must provide the user with three variations of how to close the script, so they can choose the best approach for the call.

**Variation 1: Straight to the meeting (Direktno na sastanak)**
> `...Znam da je ovo veoma "high-level" i da Vas zovem iz vedra neba, ali bih Vam bio kontakt osoba za ove stvari u budućnosti. Moja ideja je samo da zakažemo kratak uvodni razgovor krajem nedelje da se predstavim. Da li ste dostupni u [SREDA] ili [ČETVRTAK]?`

**Variation 2: Current State Question (Pitanje o trenutnom stanju)**
> `...Znam da je ovo veoma "high-level", pa me zanimalo - da li trenutno koristite neki alat ili proces koji vam pomaže da [rešite taj Pain Point]?`

**Variation 3: Validation Check (Provera validnosti)**
> `...Zvao sam samo da se predstavim. Zanimalo me je da li vam išta od ovoga zvuči poznato i koji su trenutno glavni prioriteti za vaš tim u ovoj oblasti?`

## Strict Rules
- **Language:** Serbian (Full diacritics: š, đ, č, ć, ž).
- **Tone:** Peer-to-peer. Authoritative but polite. You are an expert calling a peer, not a telemarketer begging for time.
- **Never Use:** "Da li imate minut?", "Nadam se da vas ne prekidam", "Da li je loše vreme?". (This gives away power immediately).
- **Be-Cloud Context:** Be-Cloud is a "Top 50 Microsoft Partner globalno". 

## Output Format
When executing this skill, output the generated script in a clear Markdown format, clearly separating the Pain Point analysis, the Assumptive Formality, the Value Statement, and the 3 Ask Variations.
