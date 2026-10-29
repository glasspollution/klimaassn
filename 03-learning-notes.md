# Learning notes: why the reference answer says what it says

This goes with [02-assignment-reference.html](02-assignment-reference.html). The reference shows *one* strong answer. This file explains the reasoning behind it, so you can rebuild it from your own thinking instead of copying it.

> **Don't submit the reference as-is.** Ankit asked for your core ideas in a separate note, plus honest disclosure of AI use. The goal is for you to understand every choice well enough to defend it on a call, then write your own version.

---

## 1. The spine of the answer (memorise this, not the tables)

1. **KlimaShift's product is trust in numbers.** The assignment says it outright: "we win or lose on whether our savings claims and alerts are correct."
2. **Errors are born upstream, found downstream.** A reversed clamp at install (step 3–4) shows up weeks later as a weird savings report (step 7), often spotted by the customer. → Automate *checking at the source* first.
3. **Order follows dependency:** trusted data (A+B) → savings you can defend (D) → alerts people act on (C) → renewal.
4. **Automate checking and routine; keep humans on judgement and anything the customer reads.** AI only where the task is language or images.
5. **Every claim gets a range.** "18% ± 4%" beats a bare "25%". The range is the trust feature.

If you can explain those five points on a call without notes, you own the answer.

---

## 2. Where each idea came from (evidence, not vibes)

| Idea in the doc | Evidence behind it |
|---|---|
| Mapping/install errors are real | Assignment step 4 ("each meter mapped to the right equipment"); their Ops app's latest release added QR onboarding for meters/sensors (they feel this pain); clamp-meter vendors list reversed CTs and phase mismatch as the classic causes of negative power / weird PF |
| Data health matters | Dunkin' case study: SMPS power supply dropped below 5V → irregular data, found by investigation, not automatically |
| Harsh field conditions | Dana Choga case study: voltage surges melting surge protectors |
| Savings method is the weak spot | McDonald's (25%) and Dana Choga (20%) claims publish no baseline method |
| Power factor matters in India | Maharashtra (MERC order, March 2025) moved commercial and industrial consumers >20 kW to kVAh billing. Under kVAh, poor PF directly raises the bill |
| Food safety is a non-negotiable alert class | FSSAI Schedule 4 storage temperatures (frozen −18°C, chilled ≤ ~4–5°C) for licensed restaurants |
| Simple detection first | TSB-AD benchmark (NeurIPS 2024): statistical methods often match or beat deep learning for time-series anomaly detection |

---

## 3. Concepts you must actually understand (learn in this order)

### 3.1 M&V (Measurement & Verification): the heart of Q3's deep dive
- **The question:** "How much energy *would* this store have used without us?" You can't measure that directly, so you **model it** (the *baseline*), then subtract actual use. Savings = baseline prediction − actual.
- **IPMVP options:** *Option B* = measure only the equipment you changed. *Option C* = whole-building meter (one model for the main meter). KlimaShift is mostly Option C at the main meter, with Option B-style evidence from circuit clamps.
- **Routine vs non-routine adjustments:** routine = things the model already handles (temperature, opening hours, weekday). Non-routine = one-off changes the model can't know about (new oven, renovation, store closed 3 days). Non-routine events are where savings claims usually go wrong, which is why the doc uses change-point detection plus human labelling.
- **Metrics:** **NMBE** = average bias (does the model systematically over- or under-predict?). **CV(RMSE)** = typical size of the error relative to the mean. ASHRAE Guideline 14 limits: monthly NMBE ±5% / CV(RMSE) 15%; hourly ±10% / 30%. The doc uses daily data, so it picks a threshold in between and *says it's a starting choice*.
- **Why backtest = placebo:** if you fit on weeks 1–4 and predict weeks 5–8 when *nothing changed*, true savings are zero. Any "savings" the model reports is pure error, and that is your noise floor.
- **The real-world catch (your strongest insight):** KlimaShift installs the meter on day 1, so there is **no hourly "before" data**. Hence: observation period, utility bills, and control stores within the chain.

### 3.2 Install faults you can detect from data
- **Reversed CT:** current direction flipped → active power reads **negative** on a load.
- **Phase mismatch:** CT on phase B but voltage reference from phase A → power factor looks absurd (e.g. 0.2 on a compressor) or power goes negative.
- **Switch test:** turn a machine off, see which channel drops. That's ground truth for mapping, and it's cheap.
- **Sum check:** sub-circuit channels can't add up to more than the main incomer.

### 3.3 Refrigeration signals
- **Short-cycling:** compressor starting and stopping too often (vendor rule of thumb: more than 6–10 starts per hour). Causes include a dirty condenser, a failed fan, or wrong refrigerant charge. The doc compares each unit against **its own normal** (2× its 30-day median) rather than a universal number. Different units behave differently.
- **Rising duty cycle + rising current** = a compressor working harder, an early stress signal. That's a "watch" signal, not a failure prediction.

### 3.4 Evals vocabulary
- **Precision:** of the alerts we sent, how many were real? (Low precision → alert fatigue.)
- **Recall:** of the real problems, how many did we catch? (Low recall → misses.)
- **Escaped defect:** an error that got past the check and was found later. This is the honest metric for A.
- **Golden set:** a fixed set of known cases you re-run whenever the method changes (regression testing).
- **Ground truth sources here are free:** switch tests, technician visit outcomes, one-tap feedback, utility bills, untreated stores. A big part of the answer is spotting that KlimaShift already *generates* its own labels if it captures them.

### 3.5 OSCM lens (your MBA angle; use it, it's your differentiator)
- **First-pass yield:** share of installs right the first time.
- **Lead time:** install → trusted data.
- **Bottleneck:** where errors or work pile up, not just the slowest step.
- **Cost of quality:** an error caught at the panel costs a minute; caught by the customer, it costs the account. (Prevention < appraisal < external failure.)

---

## 4. Tools: what's in, what's out, and why

**In (each solves a specific step):**
| Tool | Used for | Why this one |
|---|---|---|
| [OpenDSM](https://github.com/opendsm/opendsm) (formerly OpenEEmeter, LF Energy) | Baseline model in D | Open, standard (CalTRACK methods), approved by the US DOE for measured-savings programmes. Defensible when a customer asks "how did you calculate this?" Daily, billing and hourly models; v1.2 added uncertainty estimates for the hourly model |
| [ruptures](https://github.com/deepcharles/ruptures) | Flag non-routine events in D; step changes in B | The standard Python change-point library. Simple |
| Open-Meteo | Hourly outdoor temperature per site | Free, no key, global |
| [Docling](https://github.com/docling-project/docling) (or an LLM with vision) | Read utility bill PDFs/photos for meter-vs-bill checks | Open source, runs locally, good with tables |
| WhatsApp Business API (via providers like Interakt/Wati) + optionally n8n | Alerts with one-tap feedback in C | Store managers in India live on WhatsApp; n8n is self-hostable |

**Deliberately out (you told me not to overshoot, and this is what that looks like):**
- **Brick Schema / BuildingMOTIF** (semantic building models): powerful for big buildings with BMS systems. Overkill for a restaurant panel with 8–16 clamps.
- **Time-series foundation models** (Chronos-2 etc.): impressive, but rules + per-site baselines are easier to explain, test and trust, and the benchmarks don't say they win for this.
- **ML failure prediction:** no labels yet (listed as "not now", with a plan to collect labels).
- **Eval platforms** (Langfuse, Promptfoo, now part of OpenAI): the LLM parts here are small. A golden set in a spreadsheet plus a number-match check is enough at this stage.

**Comparables worth knowing for the call (not for the doc):** Zenatix (India, now Schneider Electric, 2,500+ buildings); Smart Joules (India, pay-from-savings); Budderfly (US, restaurant energy-as-a-service, $550M debt facility in 2026); Verdigris (US, circuit-level AI meters).

---

## 5. How to make it yours (suggested process)

1. **Before re-reading the reference**, write your own 1-page answer to Q1 in `my-core-ideas.md` from memory. What do *you* think breaks? Date it.
2. Compare it with the reference. Where you disagree, **keep your version** if you can defend it. Disagreement is good, because it's your thinking.
3. Re-score both tables (Q1, Q4) with your own weights. Your numbers will differ, and that's fine as long as you can explain them.
4. Rewrite each section in your voice. Keep the five spine points.
5. Pick your own deep-dive eval if you prefer A (commissioning). It's simpler and also valid. D is the riskier, more impressive choice.
6. Write the "Tools and AI use" line honestly.
7. Do a mock call: explain the doc out loud in 5 minutes, then answer "why not predictive maintenance first?" and "what if your week-1 audit finds no mapping errors?"

---

## Sources
- OpenDSM / OpenEEmeter: [LF Energy project](https://lfenergy.org/projects/opendsm/), [GitHub](https://github.com/opendsm/opendsm), [changelog](https://github.com/opendsm/opendsm/blob/master/CHANGELOG.md)
- ASHRAE Guideline 14 thresholds (secondary): [Unmet Hours Q&A](https://unmethours.com/question/15/when-calibrating-an-energy-model-what-are-the-typical-metrics-to-show-proper-calibration/), [energy-data.io summary](https://energy-data.io/standards/ashrae-guideline-14/)
- IPMVP options and non-routine adjustments: [EVO M&V Focus](https://evo-world.org/en/news-media/m-v-focus/847-magazine-issue-1/1068-practical-exercice-non-routine-adjustments), [NREL M&V](https://www.nrel.gov/docs/fy02osti/31505.pdf)
- Reversed CT / phase mismatch: [Continental Control Systems](https://ctlsys.com/support/negative_power_values/), [Schneider FAQ](https://www.se.com/id/en/faqs/FA203850)
- Short-cycling: [Coolrite EMS](https://coolriteems.com/blog/walk-in-cooler-compressor-short-cycling), [Lab Design News](https://www.labdesignnews.com/content/predictive-maintenance-listening-to-freezer-motors)
- kVAh billing: [Adani Electricity advisory](https://www.adanielectricity.com/blog/billing-insights/all-you-need-to-know-about-transition-to-kVAh-billing-across-maharashtra?catId=778), [IANS on MERC order](https://ianslive.in/new-kvah-billing-norms-in-merc-order-timely-action-crucial-for-commercial-industrial-consumers-in-maharashtra-lead--20250429193736)
- FSSAI storage temperatures (secondary): [Petpooja SOP guide](https://blog.petpooja.com/templates-checklist/restaurant-kitchen-sop-checklist/)
- Anomaly detection benchmark: [TSB-AD, NeurIPS 2024](https://nips.cc/virtual/2024/poster/97690)
- Chronos-2 (skipped): [Hugging Face](https://huggingface.co/amazon/chronos-2)
- Brick / BuildingMOTIF (skipped): [BuildingMOTIF docs](https://nrel.github.io/BuildingMOTIF/guides/ingress-bacnet-to-brick.html)
- ruptures: [GitHub](https://github.com/deepcharles/ruptures)
- Docling: [IBM Research](https://research.ibm.com/blog/docling-generative-AI)
- AI photo checks for installs (context): [DAC.digital fibre case](https://dac.digital/case-studies/automated-fibre-optic-installation-validation-with-computer-vision-and-machine-learning/)
- Comparables: [Zenatix/Schneider](https://www.broadcastandcablesat.co.in/zenatix-is-now-part-of-schneider-electric/), [Budderfly $550M](https://www.businesswire.com/news/home/20260325607374/en/Budderfly-Expands-Debt-Facility-to-$550-Million-to-Scale-its-Energy-as-a-Service-Platform), [Verdigris](https://en.wikipedia.org/wiki/Verdigris_Technologies), [Promptfoo → OpenAI](https://techcrunch.com/2026/03/09/openai-acquires-promptfoo-to-secure-its-ai-agents/)
