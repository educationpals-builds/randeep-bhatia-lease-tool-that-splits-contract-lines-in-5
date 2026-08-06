# Lease Duty-Splitter Audit — Five-Check Prompt Pack

Five standalone prompts for auditing a lease tool that splits contract lines into separate duties. Each prompt walks one check and ends with the measurement it demands. Use any chat model.

---

## Check 1: Unowned

**Prompt:**

You are auditing a lease tool that splits contract lines into separate duties. The tool fails on lines with conditional connectors like "provided that," "provided, however," and "unless"—it merges two duties so the wrong party looks responsible.

Here is a failing input from Harbor Lease sample contracts:

> Tenant shall repair the roof provided that Landlord funds materials within 10 days.

Walk the **Unowned** check: Is there a component explicitly responsible for detecting and handling conditional connectors before the split happens? Or does the tool assume the main parser will handle them without a dedicated step?

**Measurement demanded:** Count how many conditional-connector patterns (provided that, provided however, unless) have an explicit handler in the pipeline. Report the number and name each unowned pattern.

---

## Check 2: Copies

**Prompt:**

You are auditing a lease tool that splits contract lines into separate duties. The tool fails on lines with conditional connectors—it merges two duties so the wrong party looks responsible.

Here is a failing input from Harbor Lease sample contracts:

> Fees accrue daily; provided, however, that the cap in §4.2 still applies.

Walk the **Copies** check: Does the tool duplicate logic for handling conditional clauses in multiple places? Are there redundant rules or regex patterns that try to catch the same connector in different modules?

**Measurement demanded:** List each location where conditional-connector logic appears. Report the count of duplicated handlers and whether they produce consistent or conflicting splits.

---

## Check 3: Room

**Prompt:**

You are auditing a lease tool that splits contract lines into separate duties. The tool fails on lines with conditional connectors—it merges two duties so the wrong party looks responsible.

Here is a failing input from Harbor Lease sample contracts:

> Notice is deemed given when posted, unless the parties agree otherwise in writing.

Walk the **Room** check: When the tool encounters a conditional connector, does it have room to insert a new duty line, or does the output structure force it to append the condition to the existing duty? Can the schema accommodate two separate duty records from one input sentence?

**Measurement demanded:** Report whether the output schema allows N duties per input line. If constrained to 1:1, state the schema field that enforces the limit.

---

## Check 4: Stitch

**Prompt:**

You are auditing a lease tool that splits contract lines into separate duties. The tool fails on lines with conditional connectors—it merges two duties so the wrong party looks responsible.

Here are three failing inputs from Harbor Lease sample contracts:

> Tenant shall repair the roof provided that Landlord funds materials within 10 days.
> Fees accrue daily; provided, however, that the cap in §4.2 still applies.
> Notice is deemed given when posted, unless the parties agree otherwise in writing.

Walk the **Stitch** check: After the tool splits (or fails to split) a conditional line, does downstream processing correctly associate each duty with the right party? Or does the merge cause the summary to assign repair duty, fee caps, or notice obligations to the wrong side?

**Measurement demanded:** For each of the three sentences, trace the party assignment through to the final summary. Report how many duties end up attributed to the wrong party.

---

## Check 5: Ablation

**Prompt:**

You are auditing a lease tool that splits contract lines into separate duties. The tool fails on lines with conditional connectors—it merges two duties so the wrong party looks responsible.

Walk the **Ablation** check: Has anyone tested what happens when the conditional-connector handling is removed or disabled? Is there evidence that the current behavior is intentional, or is it an untested default?

**Measurement demanded:** Report whether ablation tests exist for conditional-connector handling. If yes, state the test name and last run date. If no, state "No ablation coverage for conditional connectors."

---

## How to use this pack

1. Pick the check most relevant to your current investigation.
2. Paste the prompt into any chat model.
3. Replace the example sentences with your own failing lease lines if needed.
4. Collect the measurement the prompt demands.
5. Repeat for all five checks to complete the audit.

---

## Sample asks

A stranger auditing their own lease-splitting tool can paste inputs like:

- "Lessee shall maintain insurance provided that Lessor approves the carrier within 30 days."
- "Rent increases annually; provided, however, that increases cannot exceed 5% per year."
- "Termination requires 60 days notice, unless both parties waive in writing."

Each prompt will walk the relevant check and return the measurement for that stranger's failing setup.

---

## Audit context from the builder

**Top crack identified:** Unowned (rated 4/4 severity)

**Ship call:** Ship with conditions: assign a lightweight keyword-flag step for "provided that," "provided, however," and "unless" as an explicit new component, run in shadow mode for a week. Priya owns the shadow review; if flagged lines don't get corrected downstream, reopen.

**Tripwire:** Watch fused-duty rate specifically on lines containing conditional connectors — target under 3%. Priya owns the dashboard; this is the only number that reflects the unowned-check gap since overall accuracy won't dip much.

**Standard for success:** Each duty lands on its own line with the right party named.

**Stakes if unfixed:** A partner signs a summary that puts repair duty on the wrong side.
