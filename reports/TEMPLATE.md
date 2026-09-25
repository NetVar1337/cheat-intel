# Trend report template

Copy to `reports/YYYY-MM-landscape.md` and fill in. Keep it short — a trend report that runs
past ~2 pages is being padded.

```markdown
# Cheat & anti-cheat landscape — YYYY-MM

**Author:** ...
**Period covered:** YYYY-MM-DD → YYYY-MM-DD
**Classification:** internal / public

## Executive summary

Three sentences maximum. What changed, what it means, what we should do.

## 1. What changed this period

### 1.1 <topic>
- **Observation:** ...
- **Evidence:** [source](url), captured YYYY-MM-DD, grade A/B/C
- **Confidence:** ...
- **Falsifier:** ...

## 2. Detection impact

| Change | Layer stressed | Existing signal catches it? | Gap / action | Owner |
|:---|:---|:---|:---|:---|
| ... | host/static/behavioral/economic | yes/no/partial | ... | ... |

## 3. Enforcement tempo

- Infection rate before last wave: ...
- Infection rate after: ...
- Time-to-adaptation (days from wave to first observed workaround): ...
- Evasion shifts observed: ...

## 4. Regional / ecosystem notes

Language- and region-specific observations. Note coverage gaps explicitly.

## 5. Negative results

What we looked for and did not find. Do not omit this section.

## 6. Open questions

What we still cannot answer, and what evidence would answer it.

## Sources

Numbered list with URLs and capture dates.
```
