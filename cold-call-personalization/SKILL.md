---
name: cold-call-personalization
description: Use when the user asks to generate a personalized cold call script, prepare for a cold call, or research a prospect to find relevant pain points for a call script. This skill enforces the Connor Murray "Who, Why, What" cold call framework for the Serbian market.
---

# Cold Call Personalization Skill (Salesmotion 2026)

## Overview
This skill is designed to generate highly personalized, high-converting cold call scripts based on the Connor Murray "Who, Why, What" framework. It is specifically tailored for the Serbian B2B market, representing Be-Cloud (direktni Microsoftov partner koji posluje u 7 zemalja Evrope).

## Step 1: Research & Info Gathering
When the user provides a lead, you must first identify their Industry and Role. Then, connect their profile strictly to Be-Cloud's two main offerings for cold calls:
1. **The Revision (Revizija licenci):** How can their specific industry benefit from a license audit? (e.g., finding unused licenses, fixing Frontline worker SKU mismatches).
2. **The "New Stuff" (Novi Microsoft alati):** What newly included Microsoft features (like Copilot, Purview, new Defender capabilities, or Teams Premium) would this specific person care about?

## Step 2: The Caller Brief (Bullet points for the user)
Before writing any script, provide the user with a short, punchy "Caller Brief". This should be 3-4 bullet points of concrete info the user can glance at and use *during* the call. It should include:
- **Industrijski rizik / Kontekst:** A specific industry trend or risk.
- **Zašto mu treba revizija:** Exactly why this person needs a license revision.
- **Relevantne Microsoft tehnologije:** Which exact Microsoft technologies (e.g., Entra ID, Intune, Purview, PowerBI, Defender for Cloud Apps) are highly relevant for their role/industry and WHY.
- **Novi alati (Udice):** Exactly which new Microsoft features to mention to them to get their attention (e.g., Copilot, Teams Premium).

## Step 2: The Script Generation
Generate the script in **Serbian**. The script MUST follow this exact structure, with NO extra fluff ("Nadam se da ste dobro", "Da li imate minut", etc.).

### A. Assumptive Formality
Always start with:
`Dobar dan [Ime], ovde Ognjen Nikolić iz Be-Clouda, kako ste?`
*(Wait for "Dobro, recite" or similar, then immediately proceed)*

### B. The Value Statement (Who, Why)
Combine the WHO and the WHY into a very short, punchy value statement focused on the revision and new features.

**Who:** `Zovem Vas jer sam deo Be-Cloud tima koji najviše sarađuje sa [Njegova Industrija] organizacijama.`
**Why:** `Trenutno radimo besplatne revizije Microsoft licenci, jer želimo da vam pokažemo neke od novih stvari i alata koje je Microsoft nedavno uključio, poput [Ubaci jedan novi "cool" feature iz Caller Briefa], a koje kompanije u vašoj industriji često već plaćaju kroz postojeće pakete a ne koriste.`

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
- **Be-Cloud Context:** Be-Cloud je direktan Microsoftov partner koji posluje u 7 zemalja Evrope. ZABRANJENO je koristiti "Top 50", "vodeći", ili bilo koji neproveriv superlativ.

## Output Format
Your output must follow this exact structure:
1. **📞 The Caller Brief:** (3-4 bullet points of highly relevant info about their industry, why they need a revision, and what new features to hook them with).
2. **📜 The Script:** (Short Assumptive Formality + Value Statement + 3 Ask Variations). Do NOT generate a long, text-heavy script. Keep it extremely concise.
