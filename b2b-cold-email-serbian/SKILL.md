---
name: b2b-cold-email-serbian
description: Use when writing personalized B2B cold emails in Serbian for Microsoft/SaaS sales outreach, generating email sequences from CRM data, or building multi-touchpoint follow-up campaigns targeting Serbian market decision-makers.
---

# B2B Cold Email - Serbian Market (Be-Cloud / Microsoft Partner)

## Overview

Battle-tested framework for writing high-conversion B2B cold emails in Serbian. Built from 100+ prospect campaigns with CRM validation, industry-specific hooks, and role-based CTAs. Core principle: **the hook determines the reply rate - everything else just doesn't break it.**

---

## ⚡ QUICK START — When User Pastes a Lead List

When the user provides a CSV or list of leads, follow this exact sequence **without asking for confirmation**:

### Step 1 — Filter (before writing anything)

Remove from the list:
- Companies with < 5 employees
- Contacts where notes contain: `ne interesuje`, `nije zainteresovan/a`, `odbio`, `odbila`, `nismo zainteresovani`, `ne zele`, `nezaint`
- Sport clubs: company name or industry contains `sport`, `klub`, `fudbal`, `košarka`, `tenis`, `atletik`
- Schools/universities: industry = `primary/secondary education`, `higher education`, `education management` OR name contains `škola`, `university`, `fakultet`, `akademija`
- State institutions / government pension funds (e.g. PIO, fond, ministarstvo) — angle doesn't apply
- Companies with no verifiable web presence (domain unresolvable)

### Step 2 — Verify hooks

For each remaining lead, scrape the company website and extract only **confirmed facts**. Use industry + role as fallback if site is unavailable. Never invent facts.

### Step 3 — Write emails

Use the **Email #1 Template** below. One email per lead.

### Step 4 — Output

- `.md` file → `/send/batch[N]_emails_may2026.md`
- `.csv` file → `/send/batch[N]_emails_may2026.csv`
- CSV columns: `First Name, Last Name, Email, Company Name, Subject, Email Body`

---

## 🔴 ABSOLUTE RULES (Never Break)

### Email Address — Source of Truth

> **Email addresses come ONLY from the user's message or the provided CSV/Excel file.**
> Never construct, guess, or derive an email address from a name and domain.
> If unsure → flag `// UNSURE - verify manually` and skip.

### No Em/En Dash

> **Never use `—` (em dash) or `–` (en dash)** anywhere in email text.
> Use regular hyphen `-`, colon `:`, or comma instead.
> These characters break rendering in some email clients.

### Serbian Diacritics

> **Always use full Serbian Unicode characters:** š, č, ć, ž, đ, Š, Č, Ć, Ž, Đ
> Never write `s` instead of `š`, `c` instead of `č/ć`, `z` instead of `ž`, `dj` instead of `đ`.

### Be-Cloud Intro — Exact Wording

> ✅ `Deo sam tima Be-Cloud, direktnog Microsoftovog partnera koji posluje u 7 zemalja Evrope.`
> ❌ "jednog od 50 vodećih Microsoft partnera globalno" — ZABRANJENO KORIŠĆENJE SUPERLATIVA KAO ŠTO JE "vodeći" ILI "top 50".
> ❌ "Radim u Be-Cloudu" — izbegavati
> ❌ "za Srbiju" — ne dodavati
> ❌ "Zovem se Ognjen Nikolić" — ime je u potpisu
> ❌ "Microsoft finansira ovaj uvodni razgovor" — zvuči kao pravdanje, ne koristiti

---

## Email #1 Template (Dan 0) — Connor Murray struktura

> **Redosled: Ko si → Zašto relevantan → Šta hoćeš**
> Primalac mora znati ko si PRE nego što pročita hook.

```
Poštovani/a [VOKATIV],

[HOOK — 2 rečenice, industry + role specific. Samo potvrđene činjenice. Bez jargona. Odmah počinjemo opservacijom/kontekstom o njihovoj industriji. PRVA REČENICA mora biti relevantna za njihov biznis.] [SPIKE — 1 rečenica koja dodaje konkretnu vrednost, problem ili "aha" momenat koji budi interesovanje. NIKAD ne koristi izmišljene brojeve, uštede ili ROI metrike koje ne možeš da verifikuješ. Zadrži spike na nivou poslovnog koncepta i rizika.]

Kao direktan Microsoftov partner, nudimo potpuno besplatnu analizu kako bismo proverili da li se ovo dešava i kod vas.

Da li Vam više odgovara sreda ([SREDA DATUM]) u 10h ili četvrtak ([ČETVRTAK DATUM]) u 14h za kratak Teams poziv?

Srdačan pozdrav,
Ognjen Nikolić
Be-Cloud | Microsoft Partner
```

**Subject:** `Microsoft licence - [Firma]`

**Zašto ovaj redosled (2026 Salesmotion Playbook):**
- Hook/Spike prvi (Context) → prva rečenica odlučuje da li se mejl čita. Mora biti o *njima* i *njihovom* problemu, ne o tebi.
- Credibility + Prelaz (Value) → U drugom paragrafu daješ kredibilitet ("direktan partner") i razlog (Risk Reversal: potpuno besplatna analiza) zašto treba da pristanu na razgovor o tom problemu, bez pravdanja.
- CTA (Ask) → jedna konkretna akcija sa specifičnim datumima.

---

## Serbian Vocative (Vokativ) — Mandatory

**Wrong:** `Poštovani Vojin` → **Correct:** `Poštovani Vojine`

| Ime | Vokativ | Pravilo |
|---|---|---|
| Branko | Branko | -o ending → no change |
| Marko | Marko | -o ending → no change |
| Darko | Darko | -o ending → no change |
| Željko | Željko | -o ending → no change |
| Nikola | Nikola | -a ending (masc) → no change |
| Milan | Milane | consonant ending → + e |
| Zoran | Zorane | consonant ending → + e |
| Stefan | Stefane | consonant ending → + e |
| Nenad | Nenade | consonant ending → + e |
| Feodor | Feodore | consonant ending → + e |
| Predrag | Predrage | consonant ending → + e |
| Vojin | Vojine | consonant ending → + e |
| Sead | Seade | consonant ending → + e |
| Milorad | Milorade | consonant ending → + e |
| Aleksandar | Aleksandre | -ar → drop a + re |
| Adel | Adele | consonant ending → + e |
| Ede | Ede | foreign/unchanged |
| Pio | Pio | foreign/unchanged |
| Benoit | Benoit | foreign/unchanged |
| Michael | Michael | foreign/unchanged |
| Ljudevit | Ljudevite | consonant ending → + e |
| Srdjan | Srđane | consonant ending → + e |
| Vladimir | Vladimire | consonant ending → + e |
| Dusan | Dušane | consonant ending → + e |
| Djordje | Đorđe | -e ending → no change |

**Female names → Poštovana [ime] (unchanged):**

- **Zlatno pravilo:** Obavezno proveriti pol pre generisanja! Ako ime završava na 'a' (uz izuzetke muških imena: Nikola, Luka, Nemanja, Ilija, Sava, Relja, Andrija, Matija, Kosta, Vanja, Saša, Mihajlo), oslovljavanje OBAVEZNO mora biti **"Poštovana"** (a ne "Poštovani").
- **Zlatno pravilo za zamenu imena i prezimena:** U CRM-u klijenti često upišu ime kao "Jankovic Milos". Pre slanja, OBAVEZNO proveri da li "First Name" polje završava na `"ić"` ili `"ic"`. Ako je tako, to znači da je u pitanju prezime i uvek ih moraš zameniti kako bi klijenta oslovio sa "Poštovani Miloše" umesto "Poštovani Jankovic".

```python
FEMALE_NAMES = {
    'Miljana','Snezana','Katarina','Jelena','Danijela','Milica',
    'Olga','Vesna','Gordana','Ana','Ivana','Jovana','Tijana',
    'Kristina','Anja','Marica','Amela','Sanja','Sofija','Olivera',
    'Dragana','Darinka','Aleksandra','Natasa','Ljubica','Nevena',
}
# Saša, Andrea, Nikola — muški kontekstualno
```

### Industry Mapping & False Friends (CRITICAL)

> **ZABRANJENO: Oslanjanje na prosti "contains" string match za industrije.** Uvek prvo detaljno mapirajte industriju.
> - `hospitality` NIJE `hospital` (npr. Hotel nema pacijente!)
> - `food production` NIJE ugostiteljstvo/turizam.
> - `automotive` (poput polovniautomobili.com) NIJE uvek "proizvodni pogon".
> - `gambling/casinos` NIJE turizam, već industrija zabave pod strogim compliance pravilima i velikim transakcijama.

---

## Hook Writing Rules

### Role → Angle

| Primalac | Hook fokus |
|---|---|
| CEO / Founder | Finansije, preplaćene licence, neiskorišćen Copilot |
| CFO | IT budžet, licencna stavka, konkretna ušteda |
| IT Manager / SysAdmin | Entra ID, neaktivni nalozi, SKU mismatch, compliance |
| COO | Terenski timovi, Frontline Worker licence |
| General Manager | Poslovni procesi, dokumentacija, revizijski trag |
| Director | Zavisi od industrije — kombinuj finansije i compliance |

### Industry → Hook tema

| Industrija | Hook tema |
|---|---|
| Pharma / Medical | Purview, kontrola pristupa, revizijski trag, GxP |
| Insurance | NBS zahtevi, digitalizacija polisa, GDPR |
| Healthcare | Zaštita medicinskih podataka pacijenata |
| Logistics / Transport | Frontline Worker licence, terenski timovi, dispečeri |
| IT / Software | Neaktivni nalozi bivših zaposlenih, SKU mismatch |
| Banking / Finance | NBS, GDPR, Microsoft Purview compliance |
| Manufacturing | Pun M365 za pogon vs. Frontline Worker tiering |
| Gaming / Gambling | Entra ID, servisni nalozi, brz rast timova |
| NGO / Dev Agencies | Microsoft Nonprofit licencni program |
| Aviation | Dokumentacijska sledljivost, revizibilnost sertifikata |
| Real Estate | Guest Access, agenti na terenu, neaktivni SharePoint |
| Engineering / Architecture | SharePoint versioning, dokumentacija, revizija |
| Consulting / Professional Services | Neaktivni nalozi bivših konsultanata, projekti |
| Energy / Oil | Terenski timovi, ad hoc licence bez plana |
| Security / Investigations | Entra ID, pristupna kontrola, audit log |
| Wholesale / Import-Export | Frontline prodajni timovi, SKU tiering |
| Water / Public Utilities | EU regulativa, dokumentacija, Purview compliance |

### Fallback (bez industrije ili titule)

> Koristi generički hook o neaktivnim nalozima bivših zaposlenih:
> *"Brzorastuće kompanije redovno dodaju Microsoft naloge pri zapošljavanju, ali retko imaju proces njihovog gašenja kada neko ode - to direktno podiže mesečni trošak."*

---

## Human Tone Rules

**Cilj:** Email koji zvuči kao da ga je čovek napisao, ne kao sales materijal.

| ❌ Ne koristiti | ✅ Koristiti |
|---|---|
| "Nadam se da ste dobro" | Direktno u temu |
| "Moje ime je Ognjen Nikolić" | Ime je u potpisu |
| "Čestitam na..." | Zvuči lažno |
| "Primetio/video sam da..." | Izveštačeno |
| "bez obaveza" | Slabi poziciju |
| "impresivno je" | Previše komplementarno |
| Cifre bez izvora ("15-25%") | Neverovidjivo |
| "uštede od 1500 evra" | Izmišljeni brojevi uništavaju kredibilitet |
| HTML, slike, linkovi | Spam filter |
| Em dash (—) ili en dash (–) | Kvari renderovanje |
| "Zovem se Ognjen..." | Ime je u potpisu |
| "Microsoft finansira ovaj razgovor" | Zvuči kao pravdanje — ne koristiti |

### Jargon koji treba izbegavati

| ❌ Jargon | ✅ Plain language |
|---|---|
| "SKU tiering" | "tip licence po korisniku" ili "licenca prilagođena ulozi" |
| "SKU mismatch" | "paket koji ne odgovara stvarnim potrebama" |
| "tenant" | izbegavati ili objasniti kontekstualno |
| "GxP", "21 CFR" | koristiti samo za IT Manager u pharma — ne za CEO/GM |

---

## Subject Lines (Naslovi emailova)

- Max **3 do 4 reči** (Connor Murray pravilo: "manje je više, jasnoća pobeđuje pametovanje").
- **Dozvoljeno (Pristup "Intro"):** `[Ime] / Ognjen - Intro`, `[Kompanija] / Be-Cloud - Intro`, ili specifičan prioritet (npr. `Copilot - [Kompanija]`).
- **Nikad:** Klikbejt procenti ("10x efficiency", "Ušteda 30%"), "Can you help me?", "revizija", "besplatno", "ponuda", "akcija". Cilj naslova je samo da se otvori mejl bez da zvuči kao sales pitch.

---

## Email Length

- Email #1: **max 120 reči**
- Follow-up #1 (Dan 3): ≤ 80 reči
- Follow-up #2 / Breakup (Dan 7): ≤ 60 reči

---

## Follow-Up Kadenca (Mandatory 4-Email Sekvenca)

**Pravilo:** 70-80% sastanaka dolazi iz follow-upova. Šalju se kao Reply unutar istog thread-a u rasponu od 7-10 dana.

### Follow-up #1 (Dan 2 ili 3) - "Nudge"
Cilj: Dati im "benefit of the doubt" i podsetiti ih na prvi mejl.
```text
Poštovani/a [VOKATIV],

Samo kratak follow-up da proverim da li je moj prethodni email stigao do Vas.

Da li Vam odgovara kratak uvodni razgovor u četvrtak ili petak pre podne?

Srdačan pozdrav,
Ognjen Nikolić
Be-Cloud | Microsoft Partner
```

### Follow-up #2 (Dan 5 ili 6) - "Slight Professional Dissatisfaction"
Cilj: Pokazati da ste prava osoba koja očekuje odgovor.
```text
Poštovani/a [VOKATIV],

Značilo bi mi Vaše mišljenje o ovome kada uhvatite malo vremena.

Srdačan pozdrav,
Ognjen Nikolić
```

### Follow-up #3 (Dan 8 ili 9) - "Assumptive Breakup"
Cilj: Blagi "guilt trip" sa pretpostavkom odlaganja.
```text
Poštovani/a [VOKATIV],

Javite mi ako ima smisla da se vratimo na ovaj razgovor kasnije. Rado ću Vas ponovo kontaktirati u [NAREDNI MESEC, npr. julu], samo trenutno planiram prioritete za naredne nedelje pa bih voleo da zatvorim ovaj krug.

Srdačan pozdrav,
Ognjen Nikolić
```

### Follow-up #4 (Dan 12) - "Last Resort / Zatvaranje"
```text
Poštovani/a [VOKATIV],

Pretpostavljam da ovo trenutno nije prioritet za [Firma], pa možemo da pauziramo ovu temu do sledećeg kvartala. 

Ako se u međuvremenu javi potreba za Microsoft podrškom, tu smo.

Srdačan pozdrav,
Ognjen Nikolić
```

---

## CTA Rules

- **Uvek sreda i četvrtak, uvek različiti sati, UVEK specifičan datum**
- Uvek izračunaj datum za **sledeću** sredu i četvrtak u odnosu na današnji dan (npr. ako je danas ponedeljak 4. maj, datumi su 6. maj i 7. maj).
- ✅ `Da li Vam više odgovara sreda (6. maj) u 10h ili četvrtak (7. maj) u 14h za kratak Teams poziv?`
- ❌ `sreda u 10h ili četvrtak u 14h` — nedostaju tačni datumi
- ❌ `sreda u 10h ili četvrtak u 10h` — isti sat, deluje kao isti slot dva puta
- ❌ `utorak ili četvrtak` — dani se ne menjaju, uvek sreda/četvrtak
- ❌ `Da li ima smisla da zakažemo...` — ostavlja prostor za NE
- ❌ `bez obaveza` — slabi poziciju

---

## Objection Handling Bank (Rad sa prigovorima preko mejla)

**Pravilo:** Preko mejla uvek **prodajemo sastanak**, ne proizvod niti rešenje. Nikada se ne raspravljamo oko tehničkih funkcionalnosti ili ko je bolji partner preko mejla.

### 1. Prigovor: "Već imamo partnera / Radimo to in-house"
**Odgovor:** 
> Poštovani [Vokativ],
> Hvala na povratnoj informaciji. Ideja ovog razgovora nije da zamenimo Vašeg trenutnog partnera ili in-house procese, već samo da se upoznamo i da imate kontakt u Be-Cloudu ukoliko se ikada pojavi specifična potreba ili zatreba dodatna ekspertiza.
> Da li bi kratak 15-minutni uvodni poziv sledeće nedelje imao smisla?

### 2. Prigovor: "Nemamo budžet za ovo"
**Odgovor:** 
> Poštovani [Vokativ],
> Potpuno razumem. Ovaj razgovor svakako nije o budžetu niti o trenutnim odlukama o kupovini. Cilj je samo upoznavanje i deljenje prakse kako bismo bili dobar resurs kada za to dođe pravo vreme.
> Da li bi kratak uvodni poziv u sredu ili četvrtak bio izvodljiv?

---

## Calendar Invites (Kalendarske pozivnice)

**Pravilo:** Pozivnica je poslednji korak da se klijent pojavi. Ako nema kontekst, zaboraviće zašto je prihvatio sastanak i možda otkazati u poslednjem trenutku.

- **Učesnici (Attendees):** Uvek jasno navesti (npr. Ognjen Nikolić - Be-Cloud, [Ime] - [Firma]).
- **Agenda:** U deskripciji invite-a OBAVEZNO staviti kratku agendu:
  1. Upoznavanje
  2. Kratak pregled trenutnog pristupa [Tema, npr. bezbednosti i licenciranju] u [Firma]
  3. Be-Cloud pregled i rešenja za industriju
  4. Naredni koraci (ukoliko ih ima)
- **Nikad:** "Hvala vam što ste izdvojili vreme", "Radujem se da naučim o vašoj ulozi", dugački marktinški tekstovi.

---

## CRM / Data Integrity

1. **Email adresa** — 100% iz korisnikove poruke ili source CSV-a. NIKAD ne konstruisati.
2. **Naziv kompanije** — ne prevoditi, ne skraćivati, ne menjati. Koristiti tačno onako kako piše.
3. **Uparivanje** — svaki kontakt ostaje sa svojim emailom. Nikad zamenjivati.
4. **Ako nisi siguran** — `// UNSURE - manually verify`, ne slati bez potvrde.

### Poznate CRM greške (uvek proveriti)

| Greška | Tačno |
|---|---|
| `Vistacom` | `Vlatacom` |
| `INNOFELT` | `INNOFILT` |
| `Tres Desperados` | `Two Desperados` |
| `VEDRA IMPEX` | `VEDIR-IMPEX` |
| `Slibo` | `Silbo` |
| `@apelapharm.rs` | `@abelapharm.rs` |

---

## Fact-Check Lista (industrije)

| Kompanija | Tačna industrija | Česta greška |
|---|---|---|
| DUNAVPLAST | Plastična ambalaža | ❌ Pharmaceuticals |
| SAVA CENTAR | Kongresni centar / events | ❌ Bolnica |
| SEDA | Razvojna agencija / NGO | ❌ Korporacija |
| Eurobank Direktna | Banka → GDPR / NBS hook | ❌ Generic financial |
| Vlatacom | Odbrambena elektronika | ❌ Civilian IT |
| Two Desperados | Ugostiteljstvo / F&B | ❌ Tres Desperados |

---

## Benchmark (2026 B2B cold email)

| Metrika | Prosek | Top performer |
|---|---|---|
| Open rate | ~27% | 40-60% |
| Reply rate | 1-5% | 15-25% |
| Meeting conversion | 1-3% | 5%+ |

Ako je reply rate < 3% → problem je relevantnost/targetovanje, ne copywriting.

---

## Referentni fajlovi

```
/Users/ognjennikolic/Documents/be-cloud selling/
  EMAIL_GENERATION_RULES.md
  data/
    validate_against_crm.py
    generate_batch3_emails.py     # Referentni generator (Batch 3, Maj 2026)
    blacklist_raw.txt             # Ne kontaktirati
  send/
    batch3_emails_may2026.md      # Poslednji čisti output
    batch3_emails_may2026.csv
  strategy/
    Cold Call Cheatsheet (Serbian).md
```
