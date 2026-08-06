# Lease tool that splits contract lines into separate duties

A lease-splitting tool that parses contract clauses into individual duties—each on its own line with the responsible party named. When lines contain conditional connectors like "provided that," "provided, however," or "unless," the tool currently merges two duties, making the wrong party look responsible.

## Verdict

**Ship with conditions:** assign a lightweight keyword-flag step for "provided that," "provided, however," and "unless" as an explicit new component, run in shadow mode for a week. Priya owns the shadow review; if flagged lines don't get corrected downstream, reopen.

## Tripwire

Watch fused-duty rate specifically on lines containing conditional connectors — target under 3%. Priya owns the dashboard; this is the only number that reflects the unowned-check gap since overall accuracy won't dip much.

## The problem

On lines with "provided that," the tool still merges two duties so the wrong party looks responsible. A partner signs a summary that puts repair duty on the wrong side.

**Standard:** Each duty lands on its own line with the right party named.

## Failing inputs

These lines from Harbor Lease sample contracts expose the failure:

```
Tenant shall repair the roof provided that Landlord funds materials within 10 days.
Fees accrue daily; provided, however, that the cap in §4.2 still applies.
Notice is deemed given when posted, unless the parties agree otherwise in writing.
```

## One-paste rebuild block

Add this keyword-flag step before the duty-splitting logic:

```
CONDITIONAL_CONNECTORS = ["provided that", "provided, however", "unless"]

def flag_conditional_lines(clause_text):
    """
    Flag any clause containing conditional connectors for manual review
    or secondary splitting pass.
    """
    flagged = False
    for connector in CONDITIONAL_CONNECTORS:
        if connector.lower() in clause_text.lower():
            flagged = True
            break
    return {
        "text": clause_text,
        "flagged": flagged,
        "requires_split": flagged
    }
```

Run in shadow mode for one week. Priya reviews flagged lines; if they don't get corrected downstream, reopen.

## What this auditor does

A stranger describes their own lease-splitting setup—what it's supposed to do, who gets hurt when it fails, and a few real failing inputs. The tool walks five checks conversationally, proposes findings with the measurement that would confirm each, and returns a scored audit with a severity story, a call, and a tripwire.

See [charter.md](charter.md) for the full audit of this specimen.  
See [METHOD.md](METHOD.md) for the five-check framework.  
See [VERIFY.md](VERIFY.md) to run verification on your own setup.

<!-- educationpals-build-verified -->
