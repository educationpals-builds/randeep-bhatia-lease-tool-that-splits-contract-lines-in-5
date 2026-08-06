# Verify: Lease tool that splits contract lines into separate duties

Use this checklist to confirm the audit tool works correctly for a stranger's own lease-splitting setup.

---

## What verification proves

A stranger with their own lease-splitting tool can run it through `/play` and receive:

1. A walk through all five checks applied to their setup
2. The **unowned** check surfaced as the deciding finding (or whichever check scores highest for their case)
3. A demand for a numeric measurement to confirm the finding

---

## Stranger verification steps

### 1. Prepare your own failing setup

Gather:
- The name of your lease-splitting tool
- What goes wrong when it fails (who gets hurt, what gets misassigned)
- Your pass/fail standard (how you'll know it's fixed)
- Three real lease lines where it fails—paste them exactly as they appear

### 2. Run through /play

Open the tool and provide your setup details when prompted. The tool will walk you through five checks conversationally.

### 3. Confirm the deciding-check finding surfaces

The tool must:
- Identify which check is the top crack for your setup
- Explain why that check matters most for your specific failure pattern
- Not skip or gloss over the deciding check

For the builder's specimen (lease tool merging duties on "provided that" lines), the deciding check was **unowned**—the tool had no component explicitly responsible for handling conditional connectors.

### 4. Confirm a numeric measurement is demanded

The tool must ask for or propose a specific number to track. Examples:

| Deciding check | Expected measurement demand |
|----------------|----------------------------|
| Unowned | Fused-duty rate on lines with conditional connectors |
| Copies | Duplicate-split percentage across contract sections |
| Room | Coverage gap on edge-case clause patterns |
| Stitch | Mismatch rate between split outputs and source duties |
| Ablation | Regression rate when removing a processing step |

For the builder's specimen, the measurement is: **fused-duty rate specifically on lines containing conditional connectors — target under 3%.**

### 5. Confirm the result includes owner and tripwire

The final audit must name:
- Who owns any conditions on the call
- Who watches the tripwire number
- What number means trouble

---

## Verification fails if

- The tool skips the deciding check or buries it among others
- No numeric measurement is proposed or demanded
- The call has conditions but no owner named
- The tripwire has no danger line or watcher

---

## Builder's worked example

**Specimen:** Lease tool that splits contract lines into separate duties

**Deciding check:** unowned

**Measurement demanded:** Fused-duty rate on lines containing conditional connectors

**Target:** Under 3%

**Watcher:** Priya owns the dashboard

A stranger's audit should follow this same structure—specific finding, specific number, specific owner.