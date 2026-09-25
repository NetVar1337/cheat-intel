<div align="center">

# cheat-intel

**Cheat-community intelligence: monitoring, trend reporting, and the intel → detection feedback loop.**

`game security` · `threat intelligence` · `cheat market` · `anti-cheat` · `OSINT`

</div>

---

## What this repo is

Anti-cheat teams do not lose to technical sophistication alone. They lose to **tempo**. A
public cheat build that lands the day after a patch, a new HWID spoofer that survives two ban
waves, a reseller network that shifts from Discord to a marketplace — each one changes what
your detections need to catch, and the change is visible in public community channels days to
weeks before it shows up in your telemetry.

This repo is the practice of **watching that surface on purpose**, and turning it into
artefacts an enforcement team can act on.

## Contents

| Path | What it is |
|:---|:---|
| [`docs/methodology.md`](docs/methodology.md) | How to collect, verify, attribute and publish community intelligence |
| [`reports/`](reports/) | Periodic trend reports, using [`reports/TEMPLATE.md`](reports/TEMPLATE.md) |
| [`collector/`](collector/) | Tooling notes for structured, repeatable collection |

## What a useful intel report contains

1. **What changed** — new cheat families, loader/delivery shifts, spoofer generations,
   peripheral/macros, account-market movements.
2. **Why it matters** — which detection layer it stresses, and which of your existing signals
   it evades.
3. **What to do** — a concrete detection or process change, with an owner.
4. **How confident we are** — sourcing grade per claim, and what would falsify it.

Reports that only restate what a forum said are not intelligence. The value is in the
*translation to detection*.

## Sourcing grades

| Grade | Meaning | Actionable? |
|:---|:---|:---|
| **A** | Primary artefact observed directly (sample, listing, official post) | Yes |
| **B** | Corroborated by two or more independent sources | Yes, with confidence interval |
| **C** | Single uncorroborated claim | No — monitor only |
| **D** | Speculation / recycling of older claims | No — drop or mark explicitly |

Most community claims arrive at grade C and are widely reported as fact. Say so in the report.

## Scope and conduct

- **Public sources only.** Public forums, public listings, vendor advisories, official game
  posts, published research.
- **No purchasing, no operating, no distributing** cheat software, accounts, or spoofers.
  Collection is observational. Buying a subscription is not "research"; it funds the operation
  you are studying and creates handling obligations you do not need.
- **No doxxing, no naming private individuals.** Report on products, services, techniques and
  infrastructure — not on the people behind handles.
- **Attribution hygiene.** Collection should not burn the account or the method. Rotate
  collection identities, never reuse operational accounts, never log in to cheat services from
  infrastructure tied to enforcement.
- **Lawful collection only.** Respect site terms where they bind, and do not access systems you
  are not permitted to access. Intelligence value does not require intrusion.

## Related

- [`apex-anticheat-lab`](https://github.com/NetVar1337/apex-anticheat-lab) — the detection
  implementations this feeds.
- [`account-security`](https://github.com/NetVar1337/account-security) — identity and account
  market abuse, which is the economic half of the same problem.
