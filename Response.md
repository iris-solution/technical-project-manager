# Take-Home Task — Technical Project Manager (OpAnalysts): Response

## 1. Assessment

Not a vendor problem. Underneath:

- **No decision owner** → design dispute unresolved at week 6, leadership chasing updates, ops asking for a demo instead of being offered one
- **10 weeks is not achievable with 3 sources** → vendor "2–3 wks, no commitment" → realistically week 9–10 → integration + validation + tuning still to come
- **Data model dispute is a symptom** → model likely assumed all 3 sources arrive together

**Biggest concern: the data we already have may be wrong.**

- Analyst doubts the 2 internal sources, which are supposedly "done"
- Unreliable data → false positives → ops learns to ignore alerts
- Unreliable data → false negatives → silent losses
- Late project = recoverable. Distrusted system = hard to recover.

## 2. Next Two Weeks

**Week 1: diagnose → reset**

- Days 1–3: 1:1s with both engineers, analyst, ops lead, sponsor, vendor → listen first, build relationships
- In parallel: timeboxed data check with analyst
  - source vs. target row counts
  - freshness, duplicates
  - consistency across the 2 internal systems
  - known historical fraud cases → are they flagged?
- Vendor: request schema / sample file / sandbox → response = real signal on timeline
- End of week: leadership update → known / unknown / proposed scope / date **range**

**Week 2: decide → build**

- Data model decision (section 3) → implement
- Demo slice on 2 internal sources
- Go-live criteria with ops + sponsor → data quality thresholds, acceptable alert volume

**Demo: keep the date, change its purpose**

- Live demo → feedback session on 2 sources, labelled as partial
- Focus: are alerts usable? → format, detail, daily volume, what ops does with each
- Feedback at week 8 → far cheaper than at go-live
- Condition: data check below minimum by day 7 → switch to workflow walkthrough on verified historical cases
- Ops informed in week 1, not the day before
- No demo on data I can't stand behind

## 3. Data Model Disagreement

Facts, not opinions. Three questions decide it:

- Does the current model break when a late source with a new schema arrives?
- Cost of rebuilding now vs. later?
- Do we know the vendor schema? → No → a rebuild now is designing blind → strongest argument against it

**Process:** separate 1:1s → joint session (each argues the other's option) → 2–3 day design spike → fixed decision date → no consensus → I decide (or the tech lead, if one exists)

**Likely outcome: middle path**

- Canonical transaction schema → internal sources map in now → vendor maps in later
- Patches isolated in per-source ingestion → never leak into detection logic

**To the rebuild engineer:** "Your concern is right. A defined boundary protects against it, and the debt is logged with an explicit trigger to revisit."

**To the patch engineer:** "Agreed, we keep moving. The patch stays isolated and documented, and you own keeping it contained."

→ No winner or loser. The point: a decision, made by a date, written down.

## 4. Escalate vs. Handle

**Principle:** trade-offs on business risk, money, or commitments I don't own → escalate, with options + a recommendation

**I handle:**

- Data model decision (within technical scope)
- Demo format + communication with ops
- Team cadence + data check
- Day-to-day technical contact with vendor

**I escalate:**

- → **Sponsor / leadership:** scope vs. date (week 10 on 2 sources, or slip for 3); acceptance of the fraud-coverage gap without vendor data → risk owner's call, not the PM's
- → **Vendor relationship owner / procurement:** contract, SLAs, leverage for a committed date → I have no relationship with the vendor
- → **Internal source system owners:** data issues traced to their systems

## 5. What I'd Verify First

- % of fraud signal from vendor feed → if most → a 2-source launch has little value → plan changes
- Is week 10 a hard constraint? (regulatory / audit / customer)
- Vendor contract terms? Schema or sample shared yet?
- Who defined the detection rules? Has ops agreed to them?
- What specific examples back the analyst's concern?
- Was there a previous PM? Why did they leave?
- Who owns go-live criteria?
