# Lease Duty-Splitter Auditor

A conversational auditor for evaluating whether a lease tool correctly splits contract lines into separate duties—especially lines containing conditional connectors like "provided that," "provided, however," and "unless."

---

## What This Auditor Does

When a stranger pastes their own failing lease-splitting setup, this auditor walks five checks, scores each, identifies the decisive gap, and returns a call with conditions and a tripwire.

---

## The Specimen Being Audited

**Tool under review:** Lease tool that splits contract lines into separate duties

**What goes wrong:** A partner signs a summary that puts repair duty on the wrong side

**Pass condition:** Each duty lands on its own line with the right party named

**Real input shape:** Old scanned leases with nested "provided that" lines

**Source:** Harbor Lease sample contracts

---

## Failing Inputs (Verbatim)

```
Tenant shall repair the roof provided that Landlord funds materials within 10 days.
Fees accrue daily; provided, however, that the cap in §4.2 still applies.
Notice is deemed given when posted, unless the parties agree otherwise in writing.
```

---

## Five-Check Ratings

| Check | Score (0–4) | Meaning |
|-------|-------------|---------|
| Unowned | 4 | Critical gap — no component owns conditional-connector splitting |
| Copies | 2 | Moderate — some duplication in parsing logic |
| Room | 2 | Moderate — limited flexibility for new clause patterns |
| Stitch | 2 | Moderate — handoff between parse and output has friction |
| Ablation | 0 | Not tested — no removal experiments run |

**Decisive check:** Unowned

---

## Ship Call

Ship with conditions: assign a lightweight keyword-flag step for "provided that," "provided, however," and "unless" as an explicit new component, run in shadow mode for a week. Priya owns the shadow review; if flagged lines don't get corrected downstream, reopen.

---

## Tripwire

Watch fused-duty rate specifically on lines containing conditional connectors — target under 3%. Priya owns the dashboard; this is the only number that reflects the unowned-check gap since overall accuracy won't dip much.

---

## How a Stranger Uses This Auditor

1. **Paste your specimen:** Describe the lease-splitting tool (or similar duty-parsing setup) you rely on. What is it supposed to do? Who gets hurt when it fails?

2. **Provide failing inputs:** Paste three or more real contract lines where the tool merges duties incorrectly or assigns the wrong party.

3. **Walk the five checks:** The auditor asks about each check in turn:
   - **Unowned:** Is there a component explicitly responsible for splitting conditional clauses?
   - **Copies:** Are there duplicate parsing paths that could diverge?
   - **Room:** Can the tool handle new clause patterns without rewrites?
   - **Stitch:** Do parsed duties hand off cleanly to the output layer?
   - **Ablation:** Have you tested what breaks when you remove components?

4. **Receive scored findings:** Each check gets a 0–4 rating with the measurement that would confirm the finding.

5. **Get the call:** Ship / ship-with-conditions / hold — with an owner on any condition.

6. **Set the tripwire:** A specific metric, a danger threshold, and who watches it.

---

## Sample Asks

A stranger with their own lease-splitting problem might paste:

> "Our contract parser handles standard clauses fine, but lines like 'Lessee maintains HVAC provided that Lessor supplies filters quarterly' come out as a single duty assigned to Lessee only. We've had two disputes this quarter where maintenance responsibility was misattributed."

> "We're splitting service agreements. 'Provider delivers reports weekly; provided, however, that Client supplies data by Monday' keeps fusing into one Provider obligation. Legal flagged three contracts last month."

> "Our duty extractor works on simple sentences but chokes on 'Party A indemnifies Party B unless Party B's negligence caused the loss.' The unless clause disappears entirely."

---

## Acceptance Criteria

- Auditor walks all five checks for a stranger's lease-splitting (or similar duty-parsing) specimen
- Every finding names the measurement that would confirm it (e.g., "count of fused-duty lines on conditional connectors")
- Each result includes a call with an owner on any condition, and an alarm with a number, a danger line, and a watcher
- The builder's own audit (Harbor Lease sample, Priya as owner, 3% fused-duty target) is visible as the worked example
