# Collector notes

How to collect repeatably without burning sources or drowning in noise.

## Principles

1. **Structured beats clever.** A scheduled, boring collection that runs every week produces
   more intelligence than an impressive one-off scrape that runs once.
2. **Collect artefacts, not opinions.** Capture, timestamp, hash, archive. Then interpret.
3. **Never let collection touch enforcement.** Separate identity, separate infrastructure,
   separate browser profile, separate network egress.
4. **Record negatives.** "Nothing found" is data.

## What to collect per source class

| Source class | Fields to capture |
|:---|:---|
| Official game / AC posts | URL, date, author, quoted metrics, enforcement categories named |
| Cheat listings | URL, capture date, product name, delivery model, price + currency, update cadence, claimed platform |
| Spoofer / hardware listings | Same, plus claimed identity fields covered and claimed detection status |
| Account markets | Price bands, account age/level offered, bulk pricing, region |
| Forum sentiment | Threads about detection status, dated; ban complaints; workaround discussion |
| Patch / game updates | Version, date, what changed in security-relevant surface |

## Storage shape

Keep it as flat, dated records — a JSONL or SQLite table per source class. The shape that
matters is: `captured_at`, `source_url`, `source_class`, `claim`, `evidence_ref`, `grade`,
`notes`.

Do not build a dashboard first. Build the records; the dashboard is a query away.

## Suggested cadence

| Task | Frequency | Time |
|:---|:---|:---|
| Official posts sweep | weekly | 20 min |
| Listing sweep (public markets/forums) | weekly | 45 min |
| Sentiment / detection-status churn | weekly | 30 min |
| Regional ecosystem sweep | monthly | 2 h |
| Report write-up | monthly | 2 h |
| Post-wave retrospective | per enforcement wave | 1 h |

## Automation

Automation is for **collection and deduplication**, not for interpretation:

- RSS / change-detection on official channels and vendor advisories — safe, reliable, automate fully.
- Listing monitors — automate capture and archiving; the classification is still human.
- Sentiment — automate *gathering*; never automate the claim into a report without a grade.

What to avoid automating: anything that posts, contacts, purchases, or authenticates to a
service. That is not collection, it is interaction, and it needs a different (and much more
careful) process.

## Handling

- Binaries you legitimately handle go in a password-protected archive with the password
  documented in your internal runbook (standard malware-handling convention: `infected`).
- Retain evidence under your organisation's retention policy.
- Be able to answer, for any line in a report: *where did this come from, when was it captured,
  and what would prove it wrong?*
