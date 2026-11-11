# Saakshi: the problem, existing solutions, and the gaps (statement 2.2)

*Research brief, 11 Nov 2026. Figures carry their sources; **estimates** are marked as such. Every claim about how the trade works must be checked in the field this week (see [field-kit.md](field-kit.md)).*

---

## 1. The statement, decoded

**Official problem (statement 2.2).**
- Jewellers issue gold to artisan goldsmiths by weight and receive finished pieces back with agreed wastage.
- Tracking issue, return, wastage, deadlines and payments across many karigars and custom orders is manual. That causes losses, disputes, missed delivery dates and late payment to artisans.
- **Today:** issues go in a notebook or on a slip, wastage is agreed verbally, deadlines are chased by phone, and accounts are squared at month end.

Between the lines, the organisers require six things:

| # | Requirement | Organisers' words | What it means for us |
|---|---|---|---|
| 1 | Weight-level accuracy | "Accuracy has to hold at the level of weight" | Integer milligrams, explicit purity, no rounding drift |
| 2 | A trail **both** sides accept | "the audit trail has to be one both parties accept" | Two-key records: every movement confirmed by giver and receiver |
| 3 | Fairness to the weaker party | "fairness matters most to the artisan, who has less power" | The karigar holds the same record; maths that doesn't accuse on noise |
| 4 | Two-party settlement | "Settlements go to both parties for approval" | Neither side can settle alone |
| 5 | Karigar's own access | "each karigar has full access to his own account" | "Mera hisab" by voice, across every jeweller they work for |
| 6 | Following the money | "A karigar with a clean record of work delivered looks very different to anyone deciding whether to trust him" | The record becomes **portable trust**: higher gold limits, credit, insurance |

The statement lists these stakeholders:
- jewellers and their counter staff;
- karigars and their helpers;
- customers with fixed occasion dates;
- refiners who recover gold from workshop scrap.

**Track rules (statement 2.2).** The system must:
- plan;
- act in external systems;
- keep memory of the case;
- recover from failures;
- seek human approval before any action involving money, legal commitment or personal data.

Sandboxed integrations are fine if disclosed. The bar is "a system that acts for its user, well beyond answering questions".

**Conditions on every solution:**
- voice-first and vernacular;
- usable with low literacy;
- works on entry-level Android;
- copes with intermittent connectivity;
- offers a JanAI Café assisted path;
- takes explicit consent and collects minimal data;
- labels its mocks.

---

## 2. How job work actually works

### The chain of custody

```
Customer order (wedding date)
      │
      ▼
Jeweller ──issue gold──► Head karigar (babu) ──► karigars ──► specialists (setting, polishing)
   ▲                                                         │
   └──────────── finished pieces + scrap ◄───────────────────┘
      │
      ├──► Hallmarking centre (AHC): purity test → HUID → sale
      └──► Refiner: workshop dust and sweepings → recovered gold
```

### How karigars work and get paid
*Source: [IIMA/XLRI, 2023](#sources), 195 interviews including 123 karigars, with fieldwork in cities including Bengaluru.*

**Workshops and output**
- Karigars are mostly Bengali-speaking migrants, working in workshops of 5–6 people run by a head karigar (*babu*).
- They work about **14 h a day, and more than 16 h in the October–December peak**.
- A karigar processes **300–400 g of gold a month**.
- Large formal firms outsource **30–50% of their manufacturing** to informal workshops.

**Pay**
- Pay is wholly or mostly variable: **wastage allowance plus making charge**.
- A karigar earns **about 1.3 g per 100 g** processed.
- Reported average informal income was ₹19,562 a month in 2023.
- **Saving wastage is part of how karigars earn.** The allowance is a negotiated term of pay, not just a loss figure.

**Allowances reported**
- **Plain work:** roughly **2–4%**.
- **Studded work:** **15–30%**.
- **Antique work:** about 4%.
- Other published norms: 3–7% for 22K work and 6–12% for 18K. DGFT's export norm (PN 30/2024-25) is 2.25% for plain handcrafted work, 4% for studded handcrafted and 0.45% for machine-made ([Tashvi](#sources)).

**How trust works**
- Trust is "the only criteria to get the job". New karigars start with **100–250 g**, and the amount grows as trust builds.
- In Kolkata the researchers found each karigar carrying **₹4–5 lakh of gold at a time** (2023 prices). Those same grams are worth more than **2×** that today.
- Reputation sits with head karigars and aggregators, who act as intermediaries for anyone without a track record.

**Payment and borrowing**
- Wages are paid in cash, often with no fixed cycle.
- Karigars have no social security and borrow from head karigars or moneylenders in emergencies.

### A worked example: why honest people still fight
Order: two 22K bangles. Agreed wastage: **4% of the fine gold issued**. Gold: 22K at about ₹13,200/g, which is about **₹14,400 per gram of fine (24K-equivalent)** ([gold rate, 30 Oct 2026](#sources)).

| Step | Gross | Purity | Fine gold |
|---|---|---|---|
| Issue to karigar | 48.250 g | 916 ‰ | **44.197 g** |
| Agreed allowance (4% of issued fine) | | | 1.768 g |
| **Fine to be returned** | | | **42.429 g** |
| Return: bangles | 45.900 g | **912 ‰** by the jeweller's XRF | 41.861 g |
| Return: scrap and filings | 0.600 g | 916 ‰ | 0.550 g |
| **Balance (jeweller's reading)** | | | **18 mg short** |
| Balance (karigar says the bangles are 916 ‰) | | | **165 mg extra** |

**What this shows**
1. **Gold must reconcile in fine weight.** Gross weight alone means nothing once alloy, solder and scrap are involved.
2. **The basis of the allowance matters.** Is it a percentage of gross or fine weight, issued or returned? It is often unstated, and that alone causes disputes.
3. **A 4 ‰ difference in purity swings the result by 184 mg, about ₹2,650.** Portable XRF readings on small, curved pieces typically land within about 0.5% of fire assay ([Thermo Fisher](#sources)).
4. **The 18 mg "shortage" is far smaller than the measurement noise.** Combining scale error (Class II scale, about ±10 mg) with purity-machine error (about ±2 ‰ on 45.9 g), the typical uncertainty on the balance is about **±105 mg**.
   - Re-testing on another XRF has the same error, so it cannot settle the question.
   - **Nobody should be accused here.** A fair system says so, and applies a rule both sides agreed beforehand for differences within the noise.
5. **Purity uncertainty dominates, not weight.** About 92 mg of the 105 mg comes from XRF, against about 9 mg from the scale. That is why "just use a better scale" doesn't fix disputes.

### Rules that shape the solution

| Rule | What it says | Design implication |
|---|---|---|
| **GST job work** (CGST s.143, Rule 55, ITC-04) | Gold can go to a job worker under a delivery challan without tax. Inputs must come back within **1 year** or the movement is treated as a supply. ITC-04 is filed **yearly** (turnover ≤ ₹5 cr) or **half-yearly** (> ₹5 cr). | Co-signed movements can produce challans and ITC-04 tables (opt-in) |
| GST on job-work charges | **5%** for Chapter 71 goods other than diamonds (1.5% for diamonds), when the karigar is registered | Settlement statements show GST when it applies |
| E-way bill | Not required for Chapter 71 goods, **except intra-state movement within Kerala** | Kerala mode later |
| **BIS hallmarking** | Fee **₹75 per gold article** since Sep 2026. If a market sample is short of fineness by **> 40 ‰**, cancellation of the jeweller's registration begins; **10–40 ‰** triggers an improved sample within 90 days. The selling jeweller pays the customer **2× the shortfall** plus testing costs. | **Purity provenance:** link each HUID back to the job, the karigar and the purity measured on return |
| Legal Metrology | Jewellers' scales must be at least **Class II** and are re-verified yearly (vendor summary; check locally) | Record scale class and stamping date; feed the permissible error into the uncertainty calculation |
| Jewellers' block insurance | Covers property held by goldsmiths up to a **memo limit**, subject to conditions such as secure lockers | Produce an insurer-ready "gold with karigars" register |
| Labour codes (in force since **21 Nov 2025**) | Make timely wage payment the norm for workers. Many karigars are piece-rate job workers, so how the codes apply to them varies. | Track per-job settlement and days-to-pay |
| **DPDP Act 2023 and Rules** (notified **14 Nov 2025**; most duties apply from about **May 2027**) | Consent, notice (in English or any Eighth Schedule language), data minimisation, erasure | Voice consent in the person's own language; erasure on request |

---

## 3. Why disputes happen: root causes

1. **One-sided records.** Only the jeweller writes, and only the jeweller holds the book. A karigar's word stands against a notebook.
2. **Invisible measurement noise.** Two scales, two XRFs, surface-only purity readings and solder joints all add error. Nobody asks whether a difference is real or just error.
3. **Wastage is pay.** Allowances are negotiated, verbal and different for every design. The base is ambiguous, and any "tightening" is a pay cut.
4. **Trust doesn't travel.** Reputation lives in head karigars' networks. Newcomers start at 100–250 g, and jewellers set exposure by gut feel.
5. **Nobody follows up.** One jeweller juggles many karigars and orders, deadlines are chased by phone, and nothing warns them early.
6. **Batch settlement in cash.** Accounts square at month end with no fixed cycle, so karigars wait weeks.
7. **A gap in power and language.** Karigars are migrants with limited literacy and 14–16 h days, speaking Bengali in Kannada- or Tamil-speaking markets. The jeweller holds the pen.
8. **Some people benefit from opacity.** On either side there is room for excess allowances, purity "adjustments" and arbitrary deductions. **Transparency must pay off for each party privately**, not just be the right thing to do.

---

## 4. How big is it?

**Jewellers and hallmarking** ([PIB summary, Nov 2026](#sources))
- **About 2.37 lakh BIS-registered jewellers.**
- **More than 65 crore gold articles hallmarked with a HUID** by 15 Oct 2026.
- Mandatory hallmarking covers **392 districts**.

**Demand** ([WGC via Outlook Money](#sources))
- India's 2025 gold jewellery demand was **430.5 t** (down 24% in volume on record prices), worth **₹4.54 lakh crore** (up 12% in value).

**Gold at risk with a single karigar**
- A karigar handles 300–400 g a month, which is about **₹40–53 lakh of 22K gold a month** at today's prices.

**The workforce**
- Bengali karigars are estimated at about **6.5 lakh** nationwide ([Telegraph](#sources)).
- About **3.5 lakh** went home from Tamil Nadu, Kerala and Karnataka in the 2020 lockdown ([Retail Jeweller India](#sources)).
- Meerut alone has **30,000+** Bengali artisans.

**Absconding cases** (a few of many)

| Where and when | What happened |
|---|---|
| Zaveri Bazaar, Mumbai, Jan 2026 | Two artisans fled with **₹98.07 lakh** of gold entrusted for ornaments (cheating and criminal breach of trust) |
| Zaveri Bazaar, Mumbai | Two artisans, **₹1.25 cr**, phones switched off |
| Mumbai | Goldsmith absconded with **2.6 kg (₹2.66 cr)** |
| Zaveri Bazaar, Mumbai, 2025 | **1,497 g** of pure gold given for mangalsutras (**₹1.30 cr**) |
| Bengaluru, 2021 | A Nagarthpet goldsmith of about 30 years took **1,104 g** from three jewellers |
| Jayanagar, Bengaluru | A goldsmith who had supplied one jeweller for four years took **1,304 g** |

**Illustration, not data.** Take a mid-size jeweller who issues 2 kg a month across 8 karigars. **0.25% of unexplained variance is 5 g, about ₹66,000 a month.** Field interviews must establish the real numbers.

---

## 5. Stakeholder map

| Stakeholder | Wants | Fears | What Saakshi gives them | Adoption risk |
|---|---|---|---|---|
| Jeweller owner | Gold back, on time, at the right purity; less time chasing | Absconding, hallmark failures, missed weddings, staff errors | Co-signed custody, gold limits, deadline agent, purity provenance, insurer and GST registers | "Accountability cuts both ways"; tax-visibility worries |
| Counter staff or manager | Fast entries, no blame | Mistakes, owner's anger | 15-second photo-and-voice entries, an audit trail that protects them | Habit |
| Head karigar (*babu*) | Steady work, bigger lots, low risk | Karigars leaving, losses they absorb | Sub-issue tracking, reputation that travels | Losing his role as intermediary |
| Karigar | Fair counting, faster pay, more work, credit | Being blamed for noise, surveillance, police or tax | Same record on their own phone, "mera hisab", fair maths, passport, per-job pay | Fear of misuse; time (14 h days) |
| Specialists (setter, polisher) | Clear accountability per stage | Blame for others' losses | Stage-level confirmations | Low volume per job |
| Customer | Piece on time for the occasion | Delay, low purity | Proactive updates (jeweller-approved), hallmark traceability | None directly |
| AHC (hallmarking centre) | Volume, fewer re-submissions | Disputes at the counter | Fewer failures; possible neutral re-test fees | Low |
| XRF or "touch" shop | Footfall, fees | — | Paid role as a neutral re-weigh and re-test point | Low |
| Refiner | Dust volume | — | Recovery certificates linked to accounts (later) | Low |
| CA | Clean data | Messy records | Challan and ITC-04 exports | Low |
| Insurer | Lower loss, proof for claims | Fraud | Custody register, limits | Partnership effort |
| Lender (PM Vishwakarma banks, NBFCs) | Low-risk borrowers, data | No credit history | Consented karigar passport | Partnership effort |
| Associations | Fewer cases, member benefits | Liability, privacy | A safer alternative to blacklists; pilot endorsement | Politics |
| JanAI Café operator | Paid services | No demand | Fee per assisted onboarding, confirmation or scheme form | Karigars are in cities; cafés are rural |

---

## 6. Existing solutions and where they fall short

| Category | Examples (public material reviewed Nov 2026) | What they do well | Where they fall short for 2.2 |
|---|---|---|---|
| **Paper** | Issue–receipt registers, slips, *bahi-khata* | Free, flexible, universal | Single copy that can be altered; no fine-gold maths; no reminders; **no karigar copy** |
| **Jewellery ERPs and billing with karigar modules** | Tally (jewellery: karigar accounting, metal-loss variation); Joolet ERP (job work, loss by % or touch, scrap and dust tracked up to refining); **Fyond** (formerly GoClixy: issue → receive → "reconcile weight on receipt", wastage per job; **₹3,500–15,000 a year**; Windows, web, Android); Vyapar (karigar job orders with material, wastage, labour); JEWELACC (fine or net weight); Jewelscore; OMGOLD; Jewell Master; Odoo module | Proper inventory and accounting; GST billing; HUID tracking in some | **Built for the jeweller only.** We found no karigar-side confirmation, copy or voice interface in their public material. They are typed, English or Hindi, and desktop- or app-first. Differences are taken at face value, with no uncertainty. They are **passive records, not agents**: no planning back from deadlines, no follow-ups, no re-planning. Nothing travels with the karigar. |
| **Karigar-facing order apps** | Logimax's "Mehta Gold Karigar" (iOS; karigars update order status for one jeweller); OrderEzy (karigar status updates); JEWELKAM; BJS Karigar | Gets karigars onto a screen for status updates | Single-company and status-only; no gold ledger; no two-party confirmation; English UI |
| **General khata apps** | OkCredit (1 crore+ downloads; a jewellery khata page), Khatabook, Vyapar | Simple; SMS and WhatsApp reminders for **money** dues | **Money only**: no grams, purity or fine; one-sided |
| **WhatsApp as a system** | Photos of slips and notebook pages; voice calls; association alert groups (CCTV images of suspects) | Universal, instant | Unstructured; no ledger or maths; alert groups carry **defamation and privacy risk** |
| **Social trust mechanisms** | Head-karigar and aggregator reputation; **community guarantees** (Meerut's karigar association: "don't give gold to any artisan without the association's guarantee"); **police verification drives** (name, addresses, relatives, phone, police station); start small at 100–250 g | Works within communities | Slow, not portable, gatekept by intermediaries, intrusive; **does nothing for honest disputes** |
| **Identity and welfare** | GJEPC **Parichay Card** (about 60,000 holders reported in 2023; subsidised health cover); **PM Vishwakarma** (Goldsmith/*Sunar* is a listed trade: collateral-free ₹1 lakh + ₹2 lakh at 5%, ₹15,000 toolkit grant); e-Shram | Identity, insurance and credit schemes exist | **Identity is not a work record.** Lenders still can't see gold handled, on-time delivery or disputes |
| **In-house manufacturing and karigar parks** | Large brands' karigar centres; **Ankurhati Gems & Jewellery Park** (Domjur, Howrah; WBIDC, about 7 acres); formal factories with departmental metal-loss accounting | Controlled environments; tight metal accounting | Capital-heavy and only for big players. Even formal firms outsource 30–50%. |
| **Insurance** | Jewellers' block policies (e.g. SBI General, Universal Sompo) with goldsmith custody under a memo limit | Pays for some losses | Doesn't prevent loss; claims need records most small jewellers don't keep |
| **Hallmarking ecosystem** | HUID per article; AHC XRF readings and weight captured automatically by the hallmarking system; HUID transfer module | Digitises purity at the point of sale | **No link back to the job or karigar** that produced the piece |

### Why it's still unsolved
1. **Builders sell to one side.** Every tool above serves the jeweller, so the record is one-sided by design. A record one party controls can never be the trail both parties accept.
2. **The karigar was never a user.** Karigars often can't type English, work 14-hour days and switch phones. Voice-first, zero-install UX on WhatsApp was not practical until voice technology covered all 22 scheduled languages, including mixed-language speech (2025–26).
3. **The maths is subtle.** Fine-gold accounting with measurement uncertainty, allowances that are really pay, and multi-stage custody are not features of generic ERPs.
4. **Neutrality is the product, and nobody built a neutral witness.** The jeweller's software is the jeweller's.
5. **Small jewellers were too costly to reach.** WhatsApp onboarding, association channels and the karigar network loop (one karigar brings in their other jewellers) now cut the cost of acquisition.

### Why now
- **Each gram is worth more than twice what it was in 2023.** The value at risk per karigar has doubled, while trust practices haven't changed.
- **Purity is now a licence risk.** BIS registration can be cancelled over market-sample shortfalls, so jewellers need purity provenance.
- **The tools have caught up.** Voice technology now covers all 22 scheduled languages, including mixed-language speech. WhatsApp and UPI are universal among migrant workers.
- **Formal norms are tightening:** labour codes (Nov 2025) and DPDP Rules (Nov 2025).
- **Good karigars are scarce.** Young people aren't joining (IIMA/XLRI), so jewellers who count fairly and pay fast will keep the best karigars.

---

## 7. From gaps to design

| Gap | Consequence | Saakshi principle | Feature |
|---|---|---|---|
| One-sided records | Word against notebook | **Two keys** | Every movement co-signed by giver and receiver (voice "haan" or button); both hold identical receipts; history is append-only |
| Typing and English | Karigars excluded | **Speak, don't type** | WhatsApp voice notes, narrated receipt cards, phone calls; photos instead of data entry |
| Noise taken as theft | False accusations, missed leaks | **Fair maths** | Fine-gold reconciliation with uncertainty; three verdicts (✅ within agreement · 🟡 within noise · 🔴 needs re-check); plain-language reasons |
| Wastage is pay | Tightening feels like theft of wages | **Contract, not suspicion** | Allowances become versioned, co-signed terms. No automatic ratchets; savings within the allowance go where the contract says. |
| Small leaks hide inside noise | Slow losses, or a mis-calibrated instrument blamed on people | **Drift detection with fair attribution** | Persistent one-sided differences are flagged. If *every* karigar shows the same bias, **flag the instrument, not the people.** |
| Passive records | Late wedding orders | **An agent that follows up** | Plans back from the occasion date, checks in by voice, re-plans with approval, keeps the customer updated |
| Trust doesn't travel | Newcomers stuck at 100–250 g; intermediaries take a cut | **Karigar-owned passport** | A verifiable, consent-based record of work delivered, shareable with jewellers, lenders and insurers |
| No exposure discipline | Absconding risk | **Limits that grow with trust** | Suggested gold limit per karigar; tranche issues; the karigar sees how to raise their own limit |
| Month-end cash settlement | Karigars wait weeks | **Settle per job** | Statement → both approve → UPI link or payout → receipt; days-to-pay tracked |
| Hallmark failures orphaned | Rework fights, BIS risk | **Purity provenance** | AHC result ↔ HUID ↔ job ↔ return purity; evidence pack; resolution both sides approve |
| Multi-stage custody | Loss falls through the cracks | **Sub-issue** | A head karigar can pass gold on with the same two-key confirmations |
| No assisted path | Feature-phone users left out | **Assisted mode** | JanAI Café or a "Saakshi point" (testing shop, association desk) confirms and onboards on someone's behalf |

## 8. What each party gets

| Party | First-week value | Long-term value |
|---|---|---|
| Jeweller | Proof of every gram out; deadlines tracked automatically | Lower losses, gold limits, purity provenance, insurer and CA registers, karigars who stay |
| Karigar | Their own copy of every issue and return; "mera hisab" anytime | Faster pay, fair counting, a passport toward higher limits, direct work and credit |
| Head karigar | Who-holds-what across their team | Reputation that travels; bigger lots |
| Customer | On-time delivery, proactive updates | Traceable purity |
| Lender or insurer | — | Consented performance data on a population they couldn't underwrite before |
| Café or Saakshi point | Fees per assisted service | A recurring service line |

## 9. Open questions we are testing in the field (12–14 Nov 2026)
1. The allowance base used in practice: percentage of issued or returned weight, gross or fine.
2. Do karigars return scrap and dust, or keep it? Who sells dust to refiners?
3. How many jewellers own an XRF, and how far apart are their readings?
4. Typical days-to-pay, and whether payment is per job or monthly.
5. Will jewellers accept karigars holding a copy? Will karigars accept being recorded?
6. Phone and WhatsApp use among karigars: smartphone share, voice-note habits.
7. Language combinations: jeweller's language versus karigar's language in each market.
8. Will jewellers share AHC results? Can they download per-HUID data?
9. Fears about tax visibility, and whether the "private between two parties" framing reassures them.
10. Willingness to pay, and who decides (owner or son).

---

## Sources
**Hackathon**
- [Tech4Bharat 2026 problem statements (PDF)](https://thegavshackathon.com/docs/Tech4Bharat-2026-Problem-Statements.pdf), statement 2.2 and the track rules.

**Karigar work, pay and trust**
- Varkkey and Jha, [*HRM Practices, Working Conditions and Labour Engagement in the Indian Gold Jewellery Manufacturing Sector*](https://www.iima.ac.in/sites/default/files/2024-04/IGPC%20funded%20project%20BVIIMAJKJXLRI-%20Final%20Report%20June2023%20%281%29.pdf), IIMA India Gold Policy Centre, June 2023.
- Wastage norms and DGFT PN 30/2024-25: [Tashvi](https://tashvi.ai/blog/jewellery-inventory-management-india-gst-karigar-old-gold).
- Bengali karigars: [Telegraph](https://obeta.ttef.in/my-kolkata/people/connecting-the-razzle-and-dazzle-of-the-maharashtra-jewellery-business-to-its-bengal-roots/cid/2024658) · [Retail Jeweller India, 2020](https://retailjewellerindia.com/return-of-gold-artisans-to-bengal-casts-shadow-over-crafts-future) · [Meerut verification drive](https://retailjewellerindia.com/meerut-bullion-traders-to-verify-artisans-credentials-before-giving-them-gold).

**Absconding cases**
- [Mumbai ₹98.07 lakh](https://www.freepressjournal.in/mumbai/mumbai-crime-2-zaveri-bazaar-gold-artisans-flee-with-jewellery-worth-9807-lakh-case-registered) · [₹1.25 cr](https://www.freepressjournal.in/mumbai/2-artisans-allegedly-flee-away-with-gold-jewellery-worth-125-cr-from-mumbais-zaveri-bazaar-search-operation-launched) · [₹2.66 cr](https://www.freepressjournal.in/mumbai/mumbai-crime-news-goldsmith-booked-for-266-crore-fraud-absconds-with-26kg-of-gold) · [₹1.30 cr](https://www.lokmattimes.com/mumbai/mumbai-goldsmith-absconds-with-gold-worth-rs13-crore-in-zaveri-bazaar-a522)
- [Bengaluru 1,104 g](https://www.deccanherald.com/amp/city/bengaluru-crime/ornament-maker-who-absconded-with-gold-from-three-jewellers-arrested-1066080.html) · [Jayanagar 1,304 g](https://www.deccanherald.com/india/karnataka/bengaluru/goldsmith-arrested-for-stealing-bullion-from-jeweller-3621564)

**Market, prices and hallmarking**
- [WGC 2025 India demand (Outlook Money)](https://www.outlookmoney.com/news/record-high-prices-pull-india-gold-demand-down-11-per-cent-in-2025-wgc) · [Gold rate, 30 Oct 2026 (Axis Max Life)](https://www.axismaxlife.com/gold-rate)
- [BIS hallmarking statistics, Nov 2026 (PIB summary)](https://superkalam.com/current-affairs/06-11-2026/bureau-of-indian-standards-hallmarking-875e59d6-9769-45e9-8d02-9aa35692c399) · [Hallmarking fee ₹75 (AIR)](https://newsonair.gov.in/bis-raises-hallmarking-charges-for-gold-articles/) · [BIS Guidelines for Jewellers, Jul 2026](https://www.bis.gov.in/wp-content/uploads/2026/07/Guidelines-for-Jewellers.pdf) · [BIS FAQ: 2× compensation](https://www.bis.gov.in/hallmarking-overview/hallmarking-faqs/mandatory/?lang=en)

**Measurement**
- XRF vs fire assay: [Thermo Fisher app note](https://assets.thermofisher.com/TFS-Assets/CAD/Application-Notes/niton-xrf-v-fire-assay-app-note.pdf) · [OneStopNDT](https://www.onestopndt.com/blogs/portable-xrf-vs-fire-assay-for-gold-analysis)
- Class II scales and permissible error: [Hindustan Scale (vendor)](https://www.hindustanscale.com/blog/what-is-government-stamping/) · [OIML R76](https://www.oiml.org/en/files/pdf_r/r076-1-e92.pdf)

**Tax and law**
- GST job work: [GJEPC presentation](https://www.gjepc.org/presentation/Job%20work%20under%20GST_Bhavin%20Mehta.pdf) · [ClearTax: ITC-04](https://cleartax.in/s/gst-inputcredit-job) · [Tally: job work](https://tallysolutions.com/gst/job-work-transactions-under-gst/) · [Chapter 71 e-way bill and Kerala (Taxscan)](https://www.taxscan.in/gstn-withdraws-e-way-bill-generation-for-chapter-71-goods-ewb-mandate-continues-in-kerala-for-intra-state-movement/488167)
- [Labour codes (PIB)](https://labour.gov.in/sites/default/files/pib2192463.pdf) · [DPDP Rules 2025 (PIB)](https://static.pib.gov.in/WriteReadData/specificdocs/documents/2025/nov/doc20251117695301.pdf)

**Insurance**
- [Universal Sompo jewellers' block wording](https://universalsompo.com/assets/file/withdrawn-products/jewellers-block-insurance-policy-wordings.pdf) · [SBI General prospectus](https://content.sbigeneral.in/uploads/Jeweller_s_Block_Insurance_Policy_Prospectus_e3c540b437.pdf)

**Existing tools**
- [Tally jewellery](https://tallysolutions.com/accounting-software/jewellery/) · [Joolet](https://joolet.com/?p=643) · [Fyond](https://fyond.com/jewellery) · [Vyapar](https://vyaparapp.in/pos-software/jewellery) · [Jewelscore article](https://dev.to/jewellery_software/can-jewellery-software-track-metal-issued-to-karigars-for-specific-designs-2455) · [Odoo module](https://apps.odoo.com/apps/modules/18.0/rg_jewelery_management_system) · [OkCredit](https://okcredit.in/khata-app-for-jewellery-shop) · [Mehta Gold Karigar](https://apps.apple.com/us/app/id1367137358) · [OrderEzy](https://apps.apple.com/ua/app/orderezy/id6474118976)

**Welfare and credit schemes**
- [GJEPC Parichay](https://gjepc.org/parichay-card.php) · [PM Vishwakarma (Bank of India)](https://bankofindia.bank.in/govt-schemes/pm-vishwakarma)
