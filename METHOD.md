# The Five-Check Method

This file explains the PRISM framework used to audit whether a setup's checks actually split the work.

---

## PRISM: Five Principles for Auditing Split-Work Setups

### P — Partition the Space

Before anything else, confirm the setup divides the input space into distinct, non-overlapping regions. Each region should map to exactly one output category. If two regions blur together—or if some inputs fall into no region at all—the partition is broken.

### R — Run in Parallel

Each check should operate independently. When checks run in sequence and hand off partial results, errors compound. Parallel checks let you isolate which one failed without untangling dependencies.

### I — Individuate the Pattern

Every check must target a specific, identifiable pattern. A check that fires on "anything unusual" isn't a check—it's a guess. Name the exact trigger: a keyword, a structure, a threshold.

### S — Stitch the Spectra

After checks run, their outputs must combine into a coherent whole. If check A says "yes" and check B says "no" for the same input, the stitching logic decides. Audit whether that logic exists and whether it handles conflicts.

### M — Map What Each Head Sees

For every check, document what it actually observes. If a check is supposed to catch conditional clauses but only sees the first five words of a line, it will miss mid-sentence connectors. Map the literal input window.

---

## The Anti-Pattern: Collapse to Monochrome

When a setup fails to partition, individuate, or stitch properly, it collapses to monochrome—treating all inputs as one undifferentiated mass. Symptoms:

- Multiple distinct duties merged into a single output line
- Responsibility assigned to whichever party appears first, regardless of clause structure
- Conditional connectors ("provided that," "unless," "provided, however") ignored entirely

Collapse to monochrome is the failure mode this audit is designed to catch. A setup that scores poorly on the five checks is likely collapsing—and the top crack identifies where the collapse begins.
