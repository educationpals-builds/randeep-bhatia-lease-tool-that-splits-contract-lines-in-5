# Audit Charter: Lease tool that splits contract lines into separate duties

## Specimen under audit

**Tool:** Lease tool that splits contract lines into separate duties

**What goes wrong if this never gets fixed:** A partner signs a summary that puts repair duty on the wrong side

**Standard for success:** Each duty lands on its own line with the right party named

---

## Real inputs tested

**Source:** Harbor Lease sample contracts

**Usage reality:** Old scanned leases with nested "provided that" lines

### Pasted failing inputs

```
Tenant shall repair the roof provided that Landlord funds materials within 10 days.
Fees accrue daily; provided, however, that the cap in §4.2 still applies.
Notice is deemed given when posted, unless the parties agree otherwise in writing.
```

---

## Check findings

| Check | Rating (0–4) |
|-------|--------------|
| Unowned | 4 |
| Copies | 2 |
| Room | 2 |
| Stitch | 2 |
| Ablation | 0 |

---

## Deciding check

**Top crack:** unowned

The unowned check scores highest (4). Conditional connectors like "provided that," "provided, however," and "unless" create split duties that no component currently owns. The tool merges them, leaving the wrong party attached to a duty.

---

## Severity story

*No severity story was provided for this audit.*

---

## Call

**Ship with conditions:** assign a lightweight keyword-flag step for "provided that," "provided, however," and "unless" as an explicit new component, run in shadow mode for a week. Priya owns the shadow review; if flagged lines don't get corrected downstream, reopen.

---

## Tripwire

Watch fused-duty rate specifically on lines containing conditional connectors — target under 3%. Priya owns the dashboard; this is the only number that reflects the unowned-check gap since overall accuracy won't dip much.

---

## Summary

This audit examined a lease tool that splits contract lines into separate duties. The tool fails on lines containing conditional connectors ("provided that," "provided, however," "unless"), merging two duties so the wrong party looks responsible.

The unowned check is the deciding gap: no component owns the job of recognizing and splitting conditional clauses. The call is to ship with conditions—a new keyword-flag step in shadow mode for one week, with Priya reviewing flagged lines. The alarm is fused-duty rate on conditional-connector lines, target under 3%, watched by Priya.
