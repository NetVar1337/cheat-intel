# Collection methodology

How to run cheat-community monitoring that produces usable intelligence rather than noise.

## 1. Define the questions first

Unstructured browsing produces unstructured reporting. Start from the decisions the team needs
to make:

- Which detection layer is about to be stressed?
- Is an enforcement wave being adapted around, and how fast?
- Is the threat shifting from software to hardware, or from PC to console?
- Is the account/economics layer being used to launder bans?

Every collection task should trace back to one of these. If it cannot, it is curiosity, and
curiosity does not belong in a report.

## 2. Source map

| Source class | What it gives you | Reliability |
|:---|:---|:---|
| Official game / AC team posts | Ground truth on enforcement, bans, incidents | A |
| Vendor / AC vendor advisories | Technical detail on detection categories | A-B |
| Public research & writeups | Technique depth, especially hardware/DMA | A-B |
| Public cheat forums and boards | What is shipping, pricing, customer sentiment | B-C |
| Marketplaces and resellers | Pricing, account supply, spoofer generations | B-C |
| Social / streaming platforms | Adoption signals, marketing claims, "UD status" claims | C |
| Patch notes and game updates | What breaks; where breakage appears first | A |

**Streaming and marketplace ecosystems vary sharply by region.** A monitoring plan that only
reads English-language forums will systematically miss the Asian cheat market, which is large
and differently distributed. Covering it needs language capability, not just translation —
slang and euphemism are where the real product names live.

## 3. Collection discipline

- **Separate collection identity from everything else.** Never from an account tied to
  enforcement, to your employer, or to your own reputation.
- **Record the artefact, not the story.** Screenshot or archive the listing, capture the URL,
  timestamp it, hash any binary you legitimately handle. A claim you cannot show is grade C.
- **Time-stamp everything.** Cheat marketing moves on days. An undated observation is close
  to useless.
- **Log what you did *not* find.** Negative results (e.g. "no new DMA listings this period")
  are often more valuable than positive ones, and they are almost never written down.

## 4. Verification

Community claims are marketing. Before promoting anything above grade C:

1. **Find an independent second source.** Not a repost of the same original.
2. **Look for contradiction.** "Undetected" claims sit alongside "banned in 2 hours" reports;
   both are usually true of different builds. Date them.
3. **Check the artefact if you can legitimately obtain one.** A listing saying "HWID spoof
   supported" is a claim; a driver sample with the corresponding IOCTL surface is evidence.
4. **State the falsifier.** For each claim, write down what observation would disprove it. If
   you cannot, it is not a testable claim and should not drive a detection change.

## 5. Translating to detection

The step most intel programmes skip. For every report item, answer:

- **Which detection layer?** Host / static / behavioral / economic
  (see the mapping table in
  [`apex-anticheat-lab/docs/cheat-taxonomy.md`](https://github.com/NetVar1337/apex-anticheat-lab/blob/main/docs/cheat-taxonomy.md)).
- **What existing signal would catch this, and did it?** If yes, this is a measurement item.
  If no, this is a detection gap with a concrete work item.
- **What is the expected evasion cost?** Does closing it force the adversary into a more
  expensive technique (e.g. from software to hardware, from hardware to account fraud)? That
  is the real goal — raise the cost, do not chase every build.

## 6. Reporting cadence

| Artefact | Cadence | Audience |
|:---|:---|:---|
| Trend report | monthly | security + game teams |
| Flash advisory | as needed | enforcement + on-call |
| Detection gap ticket | continuous | detection engineering |
| Post-wave retrospective | after each enforcement wave | security + analytics |

The retrospective is the one that makes the programme compound: measure infection rate before
and after, then ask whether the adversary adapted and how fast. That tempo number is your
actual KPI.

## 7. Handling what you find

- **Do not publish operational detail that helps evasion.** Generic technique description
  informs defenders; step-by-step configuration guides help the other side.
- **Do not name individuals.** Products, services and techniques only.
- **Escalate criminality through the right channel** (platform trust & safety, law enforcement
  referral, vendor PSIRT) rather than public confrontation.
- **Retain evidence under your own retention policy**, and be able to say where each claim in
  a report came from.
