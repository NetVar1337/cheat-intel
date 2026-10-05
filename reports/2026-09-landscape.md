# Cheat & anti-cheat landscape — 2026-09

**Period covered:** 2025-Q4 → 2026-09
**Sources:** public only (official game posts, vendor advisories, public research, public community listings)
**Status:** working baseline report. Every claim carries a grade; several widely-repeated numbers
are contested and are marked as such.

**Read this before quoting it.** Most claims below are grade B or C by this repo's own scale. Grade C is not actionable. Section 4 is a coverage gap, not coverage: English-language sources do not see the Asian streaming and marketplace ecosystems. Do not send this note as a finished intel brief. A useful brief is one primary post, one detection implication, and one thing the post does not let you conclude.

## Executive summary

Three shifts define the current period: (1) the fight has moved down the stack, from user-mode
cheats toward **hardware-assisted** and **external-input** techniques that never touch game
memory; (2) enforcement has moved **up** the stack, into hardware identity, peripheral
fingerprinting and retroactive competitive cleanup; and (3) cheat delivery is now a
subscription **service economy**, which means signature-based detection loses on tempo and
behavioral/economic detection carries the load.

## 1. What changed

### 1.1 DMA cheats are no longer a free pass

**Observation.** For several years, a second machine reading physical memory over a PCIe/FPGA
card was treated as effectively undetectable. Detection has matured across multiple vectors at
once: PCIe device enumeration with vendor/device-ID and configuration-space scrutiny, timing
characteristics, DMA-remapping (IOMMU/Vt-d) state, and known DMA-toolkit driver presence.
Public anti-cheat communications now itemise hardware bans that explicitly include DMA-class
devices rather than lumping them into "other".

**Evidence.** Community analyses of anti-cheat DMA detection [1]; public ban/enforcement
updates from Apex Legends' anti-cheat team [2][3].

**Grade:** B (technique direction corroborated; specific enforcement counts are
publisher-reported and not independently verifiable).

**Falsifier:** sustained absence of hardware-class bans in enforcement reporting while
community operators report unchanged DMA uptime.

### 1.2 Peripheral / controller emulation is now a first-class enforcement target

**Observation.** Macro and emulation devices (Cronus-class, Titan-class) that present as a
controller while running scripted recoil, rapid-fire, or mouse-aim bridging are being addressed
at the hardware/identity layer and at the distribution layer — including a notable case where a
peripheral manufacturer cooperated with a publisher to remove game-specific macro scripts from
its official distribution channels.

**Evidence.** Public enforcement communication from the Apex anti-cheat team regarding
controller/peripheral enforcement and manufacturer cooperation [2][3]; public discussion of
cross-platform detection for unauthorised controller hardware [4].

**Grade:** B for the enforcement direction; A for the manufacturer-cooperation item (it was
announced publicly).

**Falsifier:** official macro scripts reappearing in manufacturer distribution channels.

### 1.3 PC anti-cheat ownership is consolidating in-house

**Observation.** Apex Legends' PC anti-cheat moved from a third-party stack (Easy Anti-Cheat)
to an EA-owned kernel-level solution. The strategic point is not the vendor change itself —
it is **telemetry ownership**: an in-house stack lets the publisher correlate patch events,
threat intake and enforcement response on its own timeline.

**Evidence.** EA/Respawn public announcement of its kernel-level anti-cheat for Apex Legends [5].

**Grade:** A.

### 1.4 Enforcement is going retroactive and competitive-focused

**Observation.** The metrics publishers are publishing have shifted from raw ban counts toward
**competitive integrity**: ranked-point clawbacks from boosted/illegitimate accounts,
suspensions for high-rank account sharing, and a reported decline in matchmaking "infection
rate" (share of matches containing a confirmed cheater) after rolling ban waves.

**Evidence.** Public anti-cheat team updates [2][3].

**Grade:** B. The infection-rate figures quoted in the community (a decline from roughly the
mid-single-digit percentage to a lower single-digit percentage) are publisher-reported; treat
the *direction* as reliable and the *absolute numbers* as unverified.

**Falsifier:** infection rate reverting while ban volume stays constant — which would indicate
replacement-account churn rather than reduction.

### 1.5 Cheat delivery is a subscription service economy

**Observation.** Cheat distribution has professionalised: subscription pricing, per-build
encryption, automated update pipelines, and support channels. Public market research puts the
illicit cheat economy in the billions, though estimates vary by an order of magnitude depending
on what is counted (cheats only vs. cheats + accounts + infrastructure) [6][7].

**Grade:** C for any specific market figure — **these numbers are widely repeated and not
independently auditable.** Grade B for the structural observation (subscription + automated
update distribution), which is directly observable in public listings.

**Falsifier:** a shift back to one-time-purchase public builds with no update channel.

### 1.6 External / computer-vision aim is the growth area

**Observation.** Because kernel protections now cover the memory-reading path, effort has moved
to techniques that never read game memory: frame capture processed off-host (classical CV or a
small model), with input returned through a USB HID or controller emulator. Detection here is
**behavioral and device-level by necessity** — there is no binary to find on the target.

**Evidence.** Public research and analysis of kernel anti-cheat and external cheat techniques
[8][9].

**Grade:** B.

## 2. Detection impact

| Change | Layer stressed | Existing signal catches it? | Action |
|:---|:---|:---|:---|
| DMA hardware cheats | host | partial | PCIe inventory + known-good allowlist; IOMMU posture; behavioral backstop |
| Controller macro/emulation | host + behavioral | partial | HID descriptor/firmware fingerprinting; anti-recoil signature at input layer |
| External CV aim | behavioral | no (by construction) | aim kinematics + input-timing analysis is the only path |
| HWID spoofing | economic/identity | partial | cross-field fingerprint consistency, churn rate, banned-component reuse |
| Subscription delivery | static | poor, short-lived | functional-trait YARA not product hashes; accept short signature lifespans |
| Boosting / account markets | economic | no | duo-asymmetry, rank-trajectory, identity graph |

## 3. Enforcement tempo

Not measurable from public sources alone — this is the section a real programme fills from its
own telemetry. What is publicly observable is the *shape*:

- **Time-to-adaptation** appears to be days to low weeks for public cheat builds after a
  detection update, based on community "undetected"/"detected" status churn.
- **Evasion shift direction:** software → hardware → external input → identity/account fraud.
  Each shift is *more expensive* for the adversary, which is the actual objective of enforcement
  pressure, not elimination.

## 4. Regional / ecosystem notes

Coverage gap flagged. The Asian streaming and marketplace ecosystems carry a large share of
cheat distribution and account resale, and are structurally under-observed by English-language
monitoring: different platforms, different slang, different product naming conventions.
Effective coverage requires language capability, not machine translation.

## 5. Negative results

- No credible public evidence of a fully working hypervisor-resident cheat against a modern
  kernel anti-cheat being sold at retail scale in this period. Claims exist; artefacts do not.
- No public evidence that anti-cheat kernel drivers have been abused for privilege escalation at
  meaningful scale in this period. (The *theoretical* BYOVD surface remains large — see
  [`apex-anticheat-lab/host/`](https://github.com/NetVar1337/apex-anticheat-lab/tree/main/host).)
- No observed shift in the direction of server-side-only anti-cheat replacing client-side
  enforcement. The opposite: client-side kernel enforcement deepened.

## 6. Open questions

1. What fraction of hardware bans in public reporting are DMA-class vs. peripheral-class? Not
   disaggregated publicly.
2. What is the actual false-positive rate of behavioral aim detection at the thresholds that
   would be needed to catch external CV cheats? Requires labelled data, not public sources.
3. How fast does the account market replace a banned population? This is the number that
   determines whether account-level enforcement matters — see
   [`account-security`](https://github.com/NetVar1337/account-security).

## Sources

1. Community technical analysis of DMA cheat detection vectors —
   https://hwidchange.com/en/blog/how-anti-cheats-detect-dma-cheats (vendor blog; use for
   technique direction, not for vendor claims)
2. Apex Legends anti-cheat team update (2026-07-13) —
   https://forums.ea.com/blog/apex-legends-game-info-hub-en/an-update-from-the-anti-cheat-team---07132026/13556167
3. Apex Legends anti-cheat team update (2026-09-18) —
   https://www.reddit.com/r/apexlegends/comments/1wjvxt1/an_update_from_the_anti_cheat_team_09182026/
   (community mirror of an official post — verify against the EA forum original before citing)
4. Controller / peripheral enforcement discussion —
   https://www.reddit.com/r/apexlegends/comments/1w5grxp/controller_anticheat_enforcement_ban_wave_update/
5. EA announcement of kernel-level anti-cheat for Apex Legends —
   https://www.ea.com/en/games/apex-legends/apex-legends/news/javelin-anticheat-announcement
6. Anti-cheat software market reports —
   https://dataintelo.com/report/anti-cheat-software-market ·
   https://www.verifiedmarketresearch.com/product/anti-cheat-software-market/
   (**market-size figures vary widely between these; do not quote a single number**)
7. Game security industry whitepaper (2026) — https://anybrain.gg/reports/anybrain-whitepaper-2026
   (vendor publication)
8. Kernel anti-cheat technical overview — https://s4dbrd.github.io/posts/how-kernel-anti-cheats-work/
9. Gaming security trend commentary —
   https://www.cm-alliance.com/cybersecurity-blog/top-10-trends-to-ensure-secure-gaming-in-2026

---

*Sourcing note: several of these are vendor publications or community reposts. Grades are
assigned per-claim above, and a claim's grade should travel with it if this report is quoted
elsewhere.*
