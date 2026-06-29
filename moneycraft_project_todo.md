# MoneyCraft Packaged Accounts — Project To-Do

A phased roadmap from raw CSVs to a board-ready deck. The foundation work comes first because everything downstream depends on it. Steps with a *why* note are the ones easiest to get wrong — and the ones the judges will probe.

---

## Phase 0 — Orientation & setup
- [ ] Re-read the brief and the judging table; keep the five judging criteria visible as you work (storytelling, insight, fairness, commercial call, delivery).
- [ ] Load all three CSVs and inspect each: row counts, column types, date range (min/max `month`), unique channels, unique tiers, missingness per column.
- [ ] Sanity-check the headline claims against the data: does it really resolve to ~15,700 fee-paying customers, ~£1.6m annual fee revenue, ~£1.4m total spend? *If these don't reconcile, you need to know why before building anything on top.*
- [ ] Start an **assumptions & decisions log** — a running list you'll lift straight into the final "Assumptions & risks" slide.

---

## Phase 1 — Build the customer-level view (the foundation)
*This is the first real job. Everything downstream is only as fair as this table.*
- [ ] **Derive churn** — flag a customer as churned when their monthly rows stop. *Critical trap: customers still active in the final data month haven't churned — they're right-censored. Don't count them as leavers.*
- [ ] **Derive tenure** — number of active months per customer (and a join/exit month).
- [ ] **Derive value** — cumulative fees actually paid, respecting tier changes over time and £0 months during fee-waiver promos. *Value ≠ tier price × tenure, because of waivers and tier moves.*
- [ ] Capture each customer's acquisition channel, region, age band, promo flag, and their tier path (first tier, last/peak tier).
- [ ] **Join marketing spend** — aggregate spend by channel (and by month if you want time trends) to pair with customers acquired per channel.
- [ ] **Join closure reasons carefully** — decide left-join vs inner-join. *An inner join silently drops the ~third of closures with no reason, biasing everything about "why." Default to left-join and treat missing as its own category.*
- [ ] Produce one clean customer-level table: `customer_id, channel, region, age_band, tenure_months, churned (bool), total_value_£, first_tier, last_tier, joined_on_promo`.

---

## Phase 2 — Core analysis (pick what answers the question)
- [ ] **CAC by channel** = channel spend ÷ customers acquired through it.
- [ ] **LTV by channel** = expected lifetime fee revenue per customer, built from retention, not just current fees.
- [ ] **LTV:CAC by channel** — the headline value metric. *This is what separates "cheap" from "good."*
- [ ] **Churn / retention by channel** — but never rank on raw churn alone.
- [ ] **Cohort survival curves by channel** — controls for the fact that recent joiners look artificially loyal. *This is your defence against the "compare like with like" trap.*
- [ ] **The promo question** — split promo vs non-promo joiners; look at survival around month 6–7 when the fee kicks in.
- [ ] **Indexing** — which channels / tiers / segments over-represent among high-value customers.
- [ ] **Tier journey** — migration between Classic → Silver → Gold → Platinum, and which channels grow customers upward.
- [ ] **Closure reasons** — what the recorded "why" adds, and what it *can't* honestly tell you given the gaps.

---

## Phase 3 — Fairness & robustness checks (the traps, made explicit)
- [ ] Confirm every channel ranking controls for tenure/mix (not just headline averages).
- [ ] Confirm you haven't backed a channel just for being cheap (Phase 2 LTV:CAC handles this) or just for being big (volume ≠ value).
- [ ] Check whether closure-reason *missingness* differs by channel — if it does, your "why people leave" story needs caveating.
- [ ] Stress-test anything that looks too clean: re-run with a different assumption and see if the conclusion holds.

---

## Phase 4 — Synthesise into the recommendation
- [ ] Turn the analysis into **3–5 insights** — each stating what it *means* and what to *do*, not just what the data shows.
- [ ] Land **one recommendation**: where next quarter's budget goes, what to stop, and the expected payoff in pounds/customers.
- [ ] Cost it against the approved budget so the call is defensible, not hand-wavy.
- [ ] Write the **assumptions & risks**: what you assumed, and the one or two findings that would flip the call.

---

## Phase 5 — Build & rehearse the deck
- [ ] Lay out the story spine: Situation → What we found (your insights) → Recommendation → Assumptions & risks.
- [ ] One message per slide; lead with the recommendation, then earn it.
- [ ] Pick the right chart per point (e.g. survival curves for retention, a simple bar for LTV:CAC, a flow/Sankey for tier journeys) — a clear chart beats a busy table.
- [ ] Make every number mean something in £ or customers.
- [ ] Rehearse to ~10 minutes, assign speaking parts, and pre-write answers to the obvious challenge questions (the traps above are exactly where the board will push).
