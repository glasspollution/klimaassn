# KlimaShift: Company Research Brief

*Compiled 24 Oct 2026. Sources at the bottom. Confidence is marked: **[confirmed]** = company's own site/app or official registry; **[database]** = third-party profile (Tracxn, CB Insights etc.), may be stale or wrong; **[inference]** = my reading of the evidence.*

---

## 1. One-line summary

KlimaShift (formerly **Avrio / Avrio Energy**) sells a hardware + software kit that monitors and controls electricity use in **multi-outlet food & retail chains**, mostly in India, with a European foothold (Poland, Netherlands). They make money from hardware plus a monthly subscription, and win or lose on whether their savings claims and alerts hold up.

---

## 2. The company at a glance

| Item | What we know |
|---|---|
| Brand | KlimaShift (rebranded from Avrio around 2023) **[confirmed: Startup Wise Guys portfolio lists "Klimashift, formerly Avrio"]** |
| Legal entity (India) | Avrio Energy Private Limited, CIN U74999HR2017PTC071357, incorporated **6 Nov 2017**, registered office in Udyog Vihar Phase V, Gurugram (earlier Sonepat, Haryana) **[registry via Tofler]** |
| Other entities | Dutch presence in Rijsenhout / Amsterdam; a Poland team **[database]** |
| Founded (as Avrio) | 2019 per databases; the Indian company dates from 2017 **[database]** |
| Founders | **Ankit Chouhan**, Co-founder & CEO; **Puneet Kumar Batra**, Co-founder **[database + registry]**. Current directors per Tofler: Ankit Chouhan and Harshit Rai |
| Team size | Small: databases say 2–25 people. Website job posts mention "CEO, CTO, Data Analytics, and Design teams" **[database + confirmed]** |
| Hiring now | Sales Manager (Platform Solutions), Backend Developer, Operations Electrical Engineer (Diploma), all in Gurugram **[confirmed]** |
| Website language support | EN, PL, DE, NL, FR, which points to European ambitions **[confirmed: site code]** |

### About Ankit Chouhan (the person reading your assignment)
- Co-founder & CEO, Avrio Energy; **Director, PanIIT Europe – Germany**. He spoke at the PanIIT Europe Global Conference, Amsterdam, Oct 2024 **[confirmed]**
- **Juror, US Department of Energy BuildingsNEXT 2022 Design Challenge** (semifinal jurors, Attached Housing division) **[confirmed: energy.gov]**
- An aggregator site says he is an IIT Bombay alum. **Unverified**, so check his LinkedIn before mentioning it.
- What his emails show: he's direct and practical. He asked "how will you do an internship mid-semester?" and "explain in detail". He cares about **your own core ideas** over AI polish.

---

## 3. Product: what they actually sell

### The current offer (from the assignment, the most up-to-date description)
1. **Kit**: a meter with current clamps on the electrical panel, plus temperature sensors and controls on key equipment.
2. **Platform**: shows waste (equipment running overnight, freezers short-cycling, poor power factor) and flags equipment likely to fail.
3. **Business model**: hardware sale + monthly subscription. The customer expects a lower bill.

### Named product pieces
- **KlimaShift OS**: "aggregate all your building data onto one intuitive platform". Their stated four-step process is: (1) Envision use cases, (2) **real-time data validation**, (3) data normalization & workflow orchestration, (4) "Digital CX" (commissioning, checks the equipment works), **FDD** (fault detection & diagnostics), then **OSS** (optimization) **[confirmed: /how-it-works]**
- **SmartSol meter**: the meter named in the Dunkin' case study **[confirmed]**
- **Maintenance & ticketing system**: replaced Excel for Wow! Momo **[confirmed]**
- **Web platform**: platform.klimashift.com **[confirmed]**
- **KlimaShift app** (customer, Android): 1K+ downloads, 3.9★ (42 reviews), updated 21 Oct 2026. It is described as "an integrated operations management solution for businesses to manage decentralized buildings" **[confirmed]**
- **KlimaShift Operations app** (internal, for the team and partners to run audits): 10+ downloads, updated 7 Aug 2026. **Latest release: "onboard meter, sensors, and controller smoothly with QR code scanner, redundancies removed"** **[confirmed]**. This is their own fix for Step 4 ("Connect") of the assignment's workflow. They already know device-to-equipment mapping is painful.

### Website claims (treat as marketing)
- "1014 accounts connected across the globe", "5 countries", "25% coverage of India's commercial businesses utility accounts" **[confirmed as claims, not verified]**
- The /products/application page pitches a **utility-bill data aggregation** product (bill APIs, 1/5/15-minute interval data, automated bill entry, carbon tracking). The copy even refers to it as "Plugin". **[inference]** This looks like an older, software-only positioning. The assignment describes a hardware-led monitoring business, so **use the assignment as the source of truth for how they work today**, and the site for history.
- The /products/industry page claims ML "without requiring additional sensors or energy meters", which sounds like NILM (non-intrusive load monitoring). It doesn't fit the clamp-and-sensor kit described in the assignment, which is another sign the positioning has changed.

---

## 4. Customers

**Logos on the homepage** **[confirmed]**: Chaayos, Wow! Momo, KFC, McDonald's, Dana Choga, Honey Dough, Karigari, SOCIAL, Sandoz.
**Case studies also name**: Dunkin' Donuts.
**Segments in job posts**: "food retail, banking, and fuel stations".
**[inference]** KFC, McDonald's and Dunkin' in India are run by franchise operators (e.g. Devyani, Sapphire, Westlife, Jubilant), so the buyer is probably the franchisee's facilities or ops team. Ask about this rather than assume it.

### The four case studies, read with an ops lens

| Customer | Problem | What KlimaShift did | Claimed result | What it tells you for the assignment |
|---|---|---|---|---|
| **McDonald's Poland** (Jan 2024) | High energy use, HVAC/refrigeration breakdowns, no insight into peaks | Pilot at one high-traffic store: sensors on HVAC, kitchen, lighting, refrigeration; peak/off-peak scheduling; ML predictive-maintenance alerts; staff training | **25% lower energy cost; 90% fewer unplanned failures**; expanded to more stores | Large claims with **no stated baseline method**. How was 25% measured? Weather-adjusted? Footfall-adjusted? This is exactly "the catch" in the assignment (Step 7: Prove). |
| **Wow! Momo** (Mar 2022) | Maintenance and repair costs tracked in Excel across outlets | Deployed maintenance ticketing + expense tracking | "Measurable reduction", no number given | They sell an **ops/maintenance workflow product**, not just energy. Their own internal ops also run on spreadsheets (assignment). |
| **Dunkin' Donuts** (Aug 2024) | Meter data became irregular after install | Found the SMPS (meter power supply) dropping below 5V; adjusted the voltage, watched for 2 weeks, added a periodic voltage-check protocol | Accurate data restored | **Data quality failures happen in the field.** Bad data meant bad insights until someone noticed manually. A strong candidate for automation: **device/data health monitoring**. |
| **Dana Choga** (Mar 2024) | Power fluctuations; surge protectors (SPDs) overheating and melting; SMPS failures | Power conditioning, upgraded SPDs, voltage alerts, maintenance schedule, staff training | **20% lower bills; 90% less downtime** | Indian grid conditions are harsh, and the hardware and installs bear the brunt. Again, the savings figure has no stated method. |

*(Side note, keep it to yourself: the Wow! Momo case study has a copy-paste line about McDonald's, and the Electrical Engineer job post contains Backend Developer and Sales text. These are small signs of a stretched team, which supports the assignment's "a small team runs most of this manually". Don't present these as criticism. If anything, they're evidence that the team needs ops leverage.)*

---

## 5. Funding & backers

No large priced round is on record. This is a **lean, accelerator-funded company**.

| Backer | What it is | Evidence |
|---|---|---|
| **Startup Wise Guys** (Estonia) | Accelerator. Avrio was in the **2nd Wise Guys Sustainability batch**, listed as "Poland, India: AI-powered facility operating system" for SME buildings. Seed round **June 2022, SWG lead, amount undisclosed** (SWG cheques are typically €50–100K) | **[confirmed: SWG site; database for round date]** |
| **Polish government / EU funds (PARP)** | Website footer "Funded By": Fundusze Europejskie, Rzeczpospolita Polska, PARP, Unia Europejska. Most likely the **Poland Prize** soft-landing/acceleration programme for foreign startups (grants up to ~PLN 300–400K) | **[confirmed logos; programme name is inference]** |
| **Brinc** (Hong Kong) | Hardware/climate accelerator; claims Avrio targets retail with "up to 20%" opex savings | **[database; Brinc page now 404]** |
| Shell Impact Fund, Clean Cities ClimAccelerator (EIT Climate-KIC), Artesian VC | Listed by CB Insights | **[database only, unverified]** |
| **Total raised** | CB Insights: **~$160K** total, latest "Seed VC – II" | **[database]** |
| **Financials (India entity)** | Paid-up capital ₹1 lakh; operating revenue **under ₹1 crore** in FY2021-22 (growing ~60% YoY then); no registered charges (no secured debt) | **[registry via Tofler]** |

**What this means for your assignment [inference]:** "3 people and 90 days" is not hypothetical. This team is short on capital and must make every automation pay for itself quickly. Ideas that need a big data team or months of ML work before helping anyone will look naive. Ideas that **save field-ops hours, protect renewals, or make savings claims defensible** will look smart.

---

## 6. Market context worth knowing

- **Why F&B chains**: restaurants use roughly **5–7× more energy per sq ft** than other commercial buildings (refrigeration, cooking, HVAC running long hours). Chains have many small, similar sites. That's great for comparing sites, but no single site justifies an on-site energy manager.
- **India-specific**: unstable voltage and surges (see Dana Choga and Dunkin'); night-time installs because outlets run all day; diploma electricians as the field workforce; and power factor penalties or kVAh billing in many state tariffs, which is why "poor power factor" shows up as waste in the assignment. *(Check the tariff rules for the states their clients are in.)*
- **Competitors / comparables** (to learn from, not to name-drop): Zenatix (Schneider-owned, India, a direct comparable for QSR chains), Smart Joules (India, pay-for-savings model), 75F, Budderfly (US, restaurant energy-as-a-service), Arcadia (utility-data APIs, which the old KlimaShift product page resembles).
- **The "prove savings" problem has a standard name**: **M&V (Measurement & Verification)**. The industry protocol is **IPMVP**: build a baseline model (energy against weather, operating hours, footfall/sales), then compare actual use with what the baseline predicts. It's the backbone of any savings-claim eval and very likely the deep-dive eval in Q3.

---

## 7. Signals to carry into the assignment

These are **threads to pull**, not answers. The core ideas need to come from you.

1. **The company already knows Step 4 (Connect) hurts**: they just shipped QR-code device onboarding in the Ops app. What's still manual after QR? Mapping a clamp to the correct equipment and circuit, and confirming it is reading correctly.
2. **Data trust is upstream of everything**: Dunkin' shows a meter can quietly fail and the platform keeps showing numbers. If Step 4 data is wrong, Steps 5–7 (analyse, act, prove) are all wrong.
3. **Savings claims are the product**: 25% and 20% are headline numbers with no published method. A defensible, automated M&V report is both an automation target and an eval problem.
4. **Two products, one ops engine**: energy monitoring *and* maintenance ticketing (Wow! Momo). Alerts that predict failure only create value if they become tickets someone acts on.
5. **Field ops is the cost centre**: night installs, electricians, kits shipped to cities, repeat site visits for SMPS or voltage problems. Every avoided truck roll is real money for a ~$160K-funded company.

---

## 8. Questions you could ask Ankit (the assignment rewards good questions)

- How many sites are live now, across how many chains? What is a typical chain's size?
- How is the savings % computed today? Against which baseline, and normalised for what (weather, sales, menu changes, tariff changes)?
- How often is a device mis-mapped or unhealthy after install, and how is that found today?
- What share of alerts lead to an action or a ticket? Do customers ignore them?
- Who is the buyer at a franchise operator such as Devyani or Sapphire: facilities, ops, or finance? What triggers a renewal or a churn?
- Who are the "one person" dependencies today (e.g. the one engineer who can debug meters, the one person who writes savings reports)?
- Do you install controls that act automatically (e.g. scheduling), or only recommend actions to store staff?
- What does a kit cost, and how many site visits does an install take on average?

---

## Sources

- KlimaShift website: [home](https://klimashift.com/), [how it works](https://klimashift.com/how-it-works), [application product](https://klimashift.com/products/application), [industry product](https://klimashift.com/products/industry), [about](https://klimashift.com/about/company), [case studies](https://klimashift.com/resources/case-study) ([McDonald's](https://klimashift.com/resources/case-study/0), [Wow! Momo](https://klimashift.com/resources/case-study/1), [Dunkin'](https://klimashift.com/resources/case-study/2), [Dana Choga](https://klimashift.com/resources/case-study/3)), [careers](https://klimashift.com/about/career), [Electrical Engineer JD](https://klimashift.com/about/career/2)
- Google Play: [KlimaShift app](https://play.google.com/store/apps/details?id=com.avrioenergy.buildingmanager&hl=en_IN), [KlimaShift Operations app](https://play.google.com/store/apps/details?id=avrio.operation.com&hl=en_IN)
- Funding / profiles: [CB Insights](https://www.cbinsights.com/company/avrio-energy), [Tracxn – Avrio Energy](https://tracxn.com/d/companies/avrio-energy/__D7pWpbQpcaXpM2I-rrSaPlLlQj2Td0HHBEJYUbHBbpw), [Tracxn – KlimaShift](https://tracxn.com/d/companies/klimashift/__KNwvWafy2oEMBwO6niJ226rFD4itZGgjL9QWbL9R1AI), [Dealroom](https://app.dealroom.co/companies/avrio_energy_1), [PitchBook](https://pitchbook.com/profiles/company/615807-55), [Startup Wise Guys portfolio](https://startupwiseguys.com/portfolio/), [SWG 2nd Sustainability batch](https://startupwiseguys.com/news/9-sustainability-startups-to-watch-meet-the-second-wise-guys-sustainability-batch/), [Poland Prize (PARP)](https://www.parp.gov.pl/component/site/site/en-poland-prize)
- Registry: [Tofler – Avrio Energy Pvt Ltd](https://www.tofler.in/avrio-energy-private-limited/company/U74999HR2017PTC071357), [Vakilsearch](https://company.vakilsearch.com/avrio-energy-private-limited/U74999HR2017PTC071357)
- Founder: [PanIIT Europe speaker page](https://global2024.iit-europe.org/speaker/ankit-chouhan/), [DOE BuildingsNEXT 2022 jurors](https://www.energy.gov/cmei/buildings/buildingsnext/2022-design-challenge-jurors)
- Context: [Atrius – restaurant energy](https://atrius.com/restaurant-energy-savings/), [ENERGY STAR – restaurants](https://www.energystar.gov/buildings/resources-audience/small-biz/restaurants)
