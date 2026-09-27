---
title: "PulseReel: Fast-Mobilizing Content Detection & Intervention (V1)"
version: "v1.1 - Final · India Market"
---

# PulseReel: Fast-Mobilizing Content Detection & Intervention
### PRD v1.1: Final · India Market · Trust & Safety / Integrity · Owner: VP Product
### Presented by Raj Pandya

> **CONFIRMED BRIEF:** PulseReel is a short-video app with 60M Indian users aged 18–25. Its recommendation algorithm recently turned a single unverified "incident" reel into a nationwide protest movement within 72 hours, and government scrutiny of algorithmic amplification is rising. This PRD is grounded in real, current evidence (India's IT Amendment Rules, 2026; the 2018 Indian WhatsApp-lynchings precedent; documented platform incidents internationally) rather than invented facts; sourced throughout. What remains a placeholder: PulseReel has no real public brand kit, so the visual system used in this document (colors, tier badges) is my own design proposal, flagged as such, not an existing brand standard.

---

## TL;DR: What We Build, and Where the Line Is

**We build:** a real-time signal layer that scores content not on *how viral it is*, but on *how likely it is to convert into fast, real-world collective action*, using three signals in combination: (1) **velocity anomaly** relative to the content's own cohort baseline, (2) **mobilization intent** (calls to gather, replicate, boycott, or retaliate, time- or location-bound), and (3) **coordination fingerprints** (duplicate spread across many accounts in a short window, atypical for organic virality). A single signal never triggers action. All three route content into a tiered intervention ladder, from silent human-review queuing, to reduced distribution, to hard removal, with human sign-off required above a defined severity line.

**Where the line is:** V1 does **not** adjudicate truth or political viewpoint, does not act on topic sensitivity alone (protest, activism, and civic organizing are not penalized just for being civic), does not scan private messages, and does not permanently ban or remove content on an automated score alone: every Tier 3+ action requires a human reviewer within SLA. This is a deliberate position between two real, current failure modes: India's IT Amendment Rules, 2026 impose a binding 3-hour takedown deadline once a government notice arrives, but the same rules are already facing human-rights criticism for encouraging over-removal. The system is built to catch *velocity + intent + coordination*, not *virality* or *cause*, fast enough to avoid the former and precise enough to avoid the latter.

---

## 1. Problem Statement

PulseReel's recommendation system, serving 60 million users in India aged 18 to 25, is optimized to detect and amplify velocity (content spreading faster than its cohort baseline), with no separate signal for whether that spread reflects genuine real-world organizing rather than ordinary entertainment. This is not a hypothetical risk in this market: unverified viral video content has already driven rapid, lethal mob violence across India, and PulseReel's own recent incident is a direct instance of the same pattern, amplified rather than intercepted by its own algorithm; a single unverified "incident" reel escalated into a nationwide protest movement within 72 hours.

This matters to the business on two fronts simultaneously. First, India's IT (Intermediary Guidelines and Digital Media Ethics Code) Amendment Rules, 2026, in force since February 20, 2026, already compel a 3-hour takedown window on valid government notice for public-order and state-security content, with loss of safe-harbor protection for non-compliance: the cost of reactive-only detection is now a direct legal-liability clock, not just a reputational one. Second, overcorrecting with blunt, automated suppression carries its own exposure; the same 2026 Rules are already facing human-rights criticism, including from Amnesty International, for compressed takedown timelines that risk encouraging over-removal and violating free-expression protections under ICCPR Article 19. PulseReel needs to detect and differentiate fast-mobilizing content before either failure mode forces its hand.

## 2. Pain Points

| # | Pain Point | Evidence / Source |
|---|---|---|
| 1 | Cannot distinguish a mobilization-risk spike from a normal viral spike until it's already spread widely. | PulseReel's own confirmed incident, a single unverified reel escalating into a nationwide protest movement within 72 hours, is the direct, on-mechanism example: recommendation-algorithm amplification, not private forwarding. India also has an older, adjacent precedent worth citing for scale even though the propagation mechanism differs: unverified WhatsApp videos triggered mob violence across multiple states in 2018 (at least 23 deaths, 600+ arrests), spreading through private encrypted forwarding rather than public recommendation, but showing the same underlying failure mode: virality outpacing verification. Internationally: Facebook's Kenosha Guard event was reported 455 times in one day (66% of that day's total event reports) yet cleared by four moderator reviews as non-violating. |
| 2 | Escalation today is reactive, not internally detected. | The same Kenosha event was removed only hours after the shooting it was tied to had already occurred; detection followed harm rather than preceding it. |
| 3 | Blunt topic-level suppression catches legitimate speech alongside genuine risk. | Widely reported suppression of #FreePalestine-tagged content across Instagram, TikTok, X, and YouTube in 2023 affected activists, journalists, and ordinary users; the exact risk this PRD's tiered approach is designed to avoid repeating. |
| 4 | No single console; analysts stitch signals manually across systems. | Tooling fragmentation is now the single largest reported time-sink in Trust & Safety operations specifically: at TrustCon 2026, content moderation and enforcement accounted for roughly a third of practitioner "this is where we lose the most time" responses, nearly double the next-highest operational area. `[PM INPUT NEEDED]` PulseReel-specific tooling audit to confirm this pattern holds internally, not just industry-wide. |
| 5 | No pre-approved action ladder; each event negotiated ad hoc under time pressure. | Meta had no formal crisis protocol until Aug 2022, and its Oversight Board still found it too slow during the 2024 UK riots. For PulseReel this is no longer just reputational; India's IT Amendment Rules, 2026 convert "no ladder" into a binding 3-hour compliance clock once a government notice arrives. |

## 3. User Stories

| Persona | High-Level Story | Sub Stories |
|---|---|---|
| Trust & Safety Analyst | As a Trust & Safety Analyst, I want to see mobilization-risk content surfaced before it reaches broad distribution, so I can intervene while the window still matters. | • I want a live queue of high-velocity + high-intent content so I don't have to search for it manually.<br>• I want to see why something was flagged (which signals fired) so I can make a fast, defensible decision.<br>• I want to escalate a case to a Crisis Lead so severe events get faster sign-off. |
| Crisis / Policy Lead | As a Crisis Lead, I want the authority and tooling to invoke a platform-wide response to an active, fast-moving real-world event, so PulseReel doesn't amplify harm during a crisis window. | • I want to activate "Crisis Mode" on a specific claim/hashtag/audio cluster so amplification is paused platform-wide while assessed.<br>• I want an audit trail of every Crisis Mode action so we can defend the decision after the fact. |
| Content Creator | As a Creator, I want to understand if and why my content's distribution was limited, so I can adjust or appeal. | • I want an in-app notification explaining a reach restriction so I'm not left guessing.<br>• I want to appeal a restriction so a mistake can be corrected quickly. |
| Viewer | As a Viewer, I want context when I'm about to engage with content that's mobilizing real-world action, so I can make an informed choice before I share or act. | • I want a clear, non-alarmist label on content meeting the mobilization threshold so I understand what I'm looking at.<br>• I want to still be able to view content slowed for review (unless it meets the hard-removal bar) so legitimate speech isn't silently disappeared. |

## 4. Mental Model

*This section is at different confidence levels per persona, not uniformly assumed. Status is marked explicitly rather than presented as uniformly researched or uniformly guessed.*

**Analysts: CONFIRMED.** PulseReel's Trust & Safety analysts currently determine whether something is actually dangerous by **manually cross-referencing multiple dashboards and tools**: no single unified view exists today. *(Confirmed directly by the PM, not inferred.)* `[PM INPUT NEEDED]` Which specific tools they stitch together, and what they're actually looking for when they do it; that detail would sharpen this from "they cross-reference tools" to something a designer can act on directly.

**Creators: PARTIALLY CONFIRMED.** Real appeal and support-ticket language exists showing what creators believe happens when their reach is cut. *(Confirmed to exist by the PM.)* `[PM INPUT NEEDED]` The literal ticket/appeal text itself has not yet been provided. This section intentionally does not paraphrase invented creator quotes to look complete; it isn't complete until real language is dropped in here directly.

**Viewers: UNCONFIRMED.** `[ASSUMPTION – NEEDS VALIDATION]` No research has been confirmed for this persona. Working assumption only: viewers treat the feed as a single trust layer; if it's shown to me, it's been through *some* filter; with no visual language today distinguishing "this is spreading unusually fast and may be organizing real-world action" from "this is just popular." This needs real validation before GA, same as the rest of this section.

## 5. Design Requirements

**Placeholder Visual System** *(not a real PulseReel brand kit, flagged as such)*

| Token | Hex | Use |
|---|---|---|
| Ink (base) | `#0B0B0F` | App background / primary text on light surfaces |
| Signal Coral | `#FF4D6D` | Primary brand accent |
| Pulse Purple | `#7B2FF7` | Secondary brand accent, gradients |
| Calm Teal | `#14B8A6` | Tier 1: informational / low-severity |
| Safety Amber | `#FFB020` | Tier 2: friction / reduced-distribution |
| Alert Red | `#E63946` | Tier 3+: hard restriction / removal |

Tier badges are deliberately not brand-colored, so safety UI is never mistaken for a promotional or trending treatment.

**Design Block A: Viewer Context**
User Story: As a Viewer, I want to see clear, non-alarmist context on content that is spreading unusually fast and shows signs of organizing real-world action, so that I understand what I'm looking at before I share or act.
Acceptance Criteria: a user has successfully used this feature when they can:
- See a distinct visual label (Tier color, not brand color) on flagged content, separate from any "trending" badge.
- Tap the label to see a short, neutral explanation of why it's labeled, without the platform's confidence score or detection logic.
- Continue watching, sharing, or commenting on Tier 1–2 content without being blocked, unless a separate hard-violation policy also applies.
- Recognize a visually distinct, higher-severity state for Tier 3+ content (interstitial before playback), clearly different from the softer Tier 1–2 label.
- Access a "learn more" surface with links to verified sources whenever content is linked to an active, Crisis-Mode-eligible event *(V1 default: sourced only from a pre-vetted partner list maintained by Policy, e.g. news wires, public-health authorities, government emergency accounts, and independent fact-checkers; the partner list itself is a dependency tracked in §10)*.

**Design Block B: Creator Notification & Appeal**
User Story: As a Creator, I want to understand and respond to a distribution restriction on my content, so that I'm not left guessing and can correct a mistake.
Acceptance Criteria:
- Receive an in-app notification the moment a restriction is applied, written in plain language, not policy-code jargon.
- See which tier of restriction was applied and a general (not overly specific, to avoid gaming) reason category.
- Submit an appeal directly from the notification without searching Help Center.
- Track appeal status (Submitted → In Review → Resolved) in one place.
- See a restriction lift automatically: Tier 2 labels auto-expire after 24 hours of sustained signal de-escalation, or immediately on a successful appeal. Tier 3+ restrictions never auto-expire; they require explicit analyst reversal. *(V1 default.)*

**Design Block C: Analyst Console (Pulse Radar)**
User Story: As a Trust & Safety Analyst, I want a single console showing velocity, intent, and coordination signals together for flagged content, so that I can make a fast, well-informed call without stitching data manually.
Acceptance Criteria:
- See a prioritized, real-time queue of flagged content ordered by composite severity, not raw view count.
- View, for any item, which of the three signal families fired and a visual strength indicator for each.
- Watch the flagged content, its comments, and a duplicate/derivative-content cluster view without leaving the console.
- Apply, override, or escalate a tier decision directly from the console, with a mandatory short justification field.
- See a live audit trail of every action taken on the item, including by whom and when.

**Design Block D: Crisis Mode Console**
User Story: As a Crisis Lead, I want to activate and monitor a platform-wide Crisis Mode response for an active real-world event, so that amplification is paused quickly and accountably.
Acceptance Criteria:
- Search for and select the specific claim, hashtag, sound, or content cluster to place into Crisis Mode.
- See a clear preview of what Crisis Mode will and won't restrict before confirming activation.
- Require a second authorized approver before activation takes effect (two-person rule).
- Monitor real-time volume of affected content and de-escalate with the same two-person confirmation.
- See a permanent, exportable log entry for every Crisis Mode activation and deactivation.

## 6. Functional Requirements

**FR-1: Velocity Anomaly Flag**
User Story: As the system, when a piece of content's share/duplication velocity exceeds its cohort's historical baseline by a defined multiple within a defined early window, I want to flag it for signal scoring, so that mobilization-risk content is caught before broad distribution rather than after.
Functional Requirement: The system must compute a rolling velocity-anomaly score per content item, benchmarked against a dynamically computed baseline for its content cohort (creator size tier, sound/hashtag cluster, content category), and flag any item crossing the anomaly threshold within the first 15 minutes of publication.
Acceptance Criteria:
GIVEN a newly published piece of content
WHEN its share-and-duplicate velocity within the first 15 minutes exceeds its cohort baseline by more than 5x
THEN the system must create a velocity-anomaly flag record referencing that content ID
AND THEN the flag must be timestamped and passed to the Signal Scoring service within 30 seconds.
Comments: *(V1 recommended default: 15 min / 5x / 30s are a defensible starting point, not empirically validated. Data Science must recalibrate against real velocity-distribution data within the first 60 days.)* Cohort baselining logic is core domain logic Data Science must own going forward.

**FR-2: Mobilization Intent Classification**
User Story: As the system, when content contains language or audio patterns associated with time- or location-bound calls to real-world action, I want to classify it with a mobilization-intent score, so that intent is scored independently of how fast it's spreading.
Functional Requirement: The system must run an intent classifier against caption, on-screen text (OCR), spoken audio (ASR), and comment-thread text (covering Hindi and major regional Indian languages, not English alone, given the confirmed user base) to produce a mobilization-intent score (0.0–1.0 confidence) and category (e.g., gather/assemble, retaliate/target, replicate-risky-act, panic-inducing-claim).
Acceptance Criteria:
GIVEN a content item has been published in any supported language
WHEN the intent classifier processes its caption, OCR, ASR, and top-level comments
THEN it must output a mobilization-intent score and at least one intent category label if the score exceeds 0.75 confidence
AND THEN the score and category must be attached to the content's signal record, independent of the FR-1 velocity flag.
Comments: *(V1 recommended default: 0.75 is a deliberately conservative starting bar to limit false positives on ordinary civic/opinion speech.)* `[PM INPUT NEEDED]` Legal/Policy must define the authoritative intent-category taxonomy and confirm "civic organizing" is never, on its own, risk-positive. `[PM INPUT NEEDED]` Which languages to prioritize for V1 beyond Hindi, ideally set by real usage-language distribution data, not assumed here.

**FR-3: Coordination Clustering**
User Story: As the system, when near-duplicate or coordinated-posting patterns appear across many accounts in a short window, I want to generate a coordination score, so that organic virality is not confused with coordinated amplification.
Functional Requirement: The system must cluster near-duplicate content (via audio/visual/text similarity) and compute a coordination score based on posting-account diversity, account-age distribution, and posting-time concentration within the cluster.
Acceptance Criteria:
GIVEN a cluster of near-duplicate content items is detected within a rolling 30-minute window
WHEN the cluster's account-diversity and timing pattern fall outside the organic-spread distribution learned from historical data
THEN the system must assign a coordination score to every item in the cluster
AND THEN link all items in the cluster under a single Case ID for analyst review.
Comments: *(V1 recommended default: 30 min balances catching fast coordination against needing enough postings to form a statistically meaningful cluster.)* Requires a labeled historical dataset of known-organic vs. known-coordinated spread events to calibrate, flagged as a hard dependency in §10; this gates V1 timeline until confirmed.

**FR-4: Composite Tiering**
User Story: As the system, when velocity, intent, and coordination scores combine to cross defined severity thresholds, I want to assign a content item to an intervention tier, so that action is proportionate and consistent rather than ad hoc.
Functional Requirement: The system must compute a composite severity tier (0–4, per the TL;DR ladder) from the three independent signal scores using a defined combination rule, and must never assign Tier 2+ from a single signal family alone.
Acceptance Criteria:
GIVEN a content item has velocity, intent, and coordination scores attached
WHEN at least two of the three signal families exceed their respective thresholds
THEN the system must assign a Tier 1 or higher classification per the combination table below
AND THEN content with only one signal family elevated must be capped at Tier 1, never routed to automatic distribution restriction.

**V1 Recommended Tier Combination Table:**

| Signals Elevated | Assigned Tier | Action |
|---|---|---|
| 0 of 3 | Tier 0 | Normal distribution, no action |
| Exactly 1 of 3 | Tier 1 | Silent observation queue only, no user-visible change |
| Exactly 2 of 3 (any combination) | Tier 2 | Reduced amplification + visible label; auto-notify creator |
| All 3 of 3 | Tier 3 | Distribution frozen; mandatory human review (Pulse Radar) |
| All 3 of 3 AND high-severity intent category (imminent violence / self-harm replication / panic claim tied to a live, verified crisis) | Tier 4-eligible | Routed directly to Crisis Lead for possible Crisis Mode (FR-6) |

Comments: *(V1 recommended default.)* This table is the single most important business-logic decision in this PRD. It is proposed as a defensible starting position (not yet empirically validated) and must be formally signed off by Policy + Data Science before GA, then revisited using real precision/recall data per §9.

**FR-5: Human Sign-Off Above Tier 3**
User Story: As the system, when content is assigned Tier 3 or higher, I want to require human analyst sign-off before any distribution-restricting action is applied, so that no high-impact action is taken on automated scoring alone.
Functional Requirement: The system must block automatic execution of any Tier 3+ action and route the case to the Pulse Radar analyst queue, holding the item in its current distribution state pending human decision, unless a pre-approved Crisis Mode playbook applies.
Acceptance Criteria:
GIVEN a content item is scored as Tier 3 or higher
WHEN the scoring engine attempts to apply the corresponding action
THEN the system must instead create a pending-review case in the Pulse Radar queue
AND THEN the item's current distribution state must remain unchanged until an analyst records a decision
AND WHEN no analyst decision is recorded within 30 minutes (Tier 3) or 10 minutes (Tier 4-eligible)
THEN the case must auto-escalate to the on-call Crisis Lead.
Comments: *(V1 recommended default.)* These SLAs are deliberately set well inside India's IT Amendment Rules, 2026 3-hour statutory takedown deadline (see §8), and deliberately so, so human review completes with margin before that becomes the forcing function. They're still only meaningful if 24/7 Pulse Radar coverage is actually staffed to meet them, a real open dependency tracked in §10.

**FR-6: Crisis Mode Activation**
User Story: As a Crisis Lead, when I activate Crisis Mode on a specific content cluster, I want the restriction to apply platform-wide to that cluster only, so that response is fast without over-broadly suppressing unrelated content.
Functional Requirement: The system must allow an authorized Crisis Lead to apply a distribution-pause action scoped to a specific Case ID/content cluster, requiring a second authorized approver before the action takes effect.
Acceptance Criteria:
GIVEN an authorized Crisis Lead selects a Case ID and requests Crisis Mode activation
WHEN a second authorized approver confirms the request
THEN the system must apply the distribution-pause to every content item currently linked to that Case ID
AND THEN log the activation, both approvers' identities, and a timestamp to an immutable audit record
AND WHEN the Crisis Lead requests deactivation
THEN the same two-approver confirmation must be required before distribution resumes.
Comments: Crisis Mode is PulseReel's own proactive tool, distinct from, and intended to reduce reliance on, the reactive, government-notice-triggered 3-hour takedown process under India's IT Amendment Rules, 2026 (see §8).

**FR-7: Creator Notification & Appeal Routing**
User Story: As a Creator, when my content is restricted at Tier 2 or higher, I want to be notified and able to appeal, so that legitimate content isn't silently suppressed.
Functional Requirement: The system must send an in-app notification to the content owner within a defined window of any Tier 2+ action and expose an appeal submission flow linked to that specific action.
Acceptance Criteria:
GIVEN a Tier 2 or higher action is applied to a content item
WHEN the action is recorded
THEN the system must notify the content owner within 15 minutes with a plain-language reason category
AND THEN the owner must be able to submit an appeal referencing that action ID
AND WHEN an appeal is submitted
THEN it must be routed to a queue distinct from the original detection queue, to avoid the same analyst rubber-stamping their own decision.
Comments: None.

## 7. Solution User Flow

**Flow A: Content lifecycle through detection & intervention**
1. **Publish**: Creator publishes content; it enters normal distribution immediately (no default delay).
2. **Signal computation** (background, ~continuous): Velocity (FR-1), intent (FR-2), and coordination (FR-3) scores compute in parallel. *Decision point:* if none cross threshold → standard ranking, no further flow.
3. **Tiering** (FR-4): If ≥2 signal families cross threshold, item is assigned a tier: Tier 0–1 continues distributing (Tier 1 silently added to the Observation list); Tier 2 gets reduced amplification + label, Creator notified (Flow C), Viewer sees label (Flow B); Tier 3+ routes to Pulse Radar (Flow D), distribution frozen. **Loop:** no analyst action within SLA → auto-escalates to Crisis Lead (FR-5), who can invoke Flow E.
4. **Resolution**: Analyst/Crisis Lead decision writes back to the content record. **Loop:** a cleared false positive returns to Tier 0 and closes the case; a fresh anomaly can re-open a new case.

**Flow B: Viewer encountering flagged content**
1. **Feed**: Viewer sees content with a Tier-color label overlay (Tier 1: none visible; Tier 2: label chip; Tier 3+: full-screen interstitial before playback).
2. **Tap label** (Tier 2) → Context sheet opens with neutral explanation + verified-source links if crisis-linked → Viewer continues or dismisses → returns to feed.
3. **Interstitial** (Tier 3+) → Viewer sees restriction notice, can view profile/original context, content is not auto-played or pushed further → can back out to feed (no forced continuation).

**Flow C: Creator notified of restriction**
1. **Notification received** → Creator taps → Restriction detail screen (tier, plain-language reason, timestamp).
2. *Decision point:* Creator taps **Appeal** → Appeal form → Submitted confirmation → Status tracker (Submitted → In Review → Resolved). **Loop:** Creator can return to the tracker anytime until resolved.
3. Alternatively, Creator taps **Learn more about this policy** → Help Center article (no appeal filed) → flow ends.

**Flow D: Analyst working the Pulse Radar queue**
1. **Queue view** (sorted by composite severity) → Analyst selects a case → Case detail console (content player + signal breakdown + duplicate-cluster view + comment sample).
2. *Decision point:* Analyst selects **Uphold Tier**, **Downgrade**, **Clear (false positive)**, or **Escalate to Crisis Lead** → mandatory justification field → Confirm.
3. Action writes back to the content record (Flow A, step 4) → case moves to Resolved. **Loop:** Analyst can reopen a resolved case if new duplicate-cluster activity links to it.

**Flow E: Crisis Lead invoking Crisis Mode**
1. **Escalated case received** (from Flow D or FR-5 auto-escalation) → Crisis Mode console → Crisis Lead reviews cluster scope preview.
2. **Request activation** → routed to second approver → Approver confirms → Crisis Mode live; console shows real-time affected-volume monitor.
3. *Decision point:* Crisis Lead **maintains** Crisis Mode or **requests deactivation** → second approver confirms → distribution resumes → **loop** back to Flow A, step 2, for remaining items (they re-enter normal signal computation).

## 8. Non-Functional Requirements

- **Latency:** Signal scores must refresh on a rolling basis at least every 2 minutes post-publication, so a Tier 1+ flag can surface as early as the data supports; no later than the 15-minute checkpoint in FR-1. *(V1 recommended default.)*
- **Scale:** The signal pipeline must scale horizontally to PulseReel's full daily upload volume and add no more than 50ms p95 latency to the standard ranking pipeline. *(V1 recommended default: exact infrastructure sizing needs current upload-volume figures from Engineering, not assumed here.)*
- **Availability:** Pulse Radar console and Crisis Mode activation must target 99.9% uptime; an outage here should not silently allow Tier 3+ auto-actions without a documented fail-safe. *(V1 recommended default.)*
- **Fail-safe behavior:** If Signal Scoring or Tiering is unavailable, content must default to **normal distribution with no restriction** (fail-open, never fail-closed) so an outage never silently suppresses legitimate content platform-wide. `[ASSUMPTION – NEEDS VALIDATION]` This is my explicit recommendation as the tradeoff that best protects expression during an outage, but it still needs Policy/Legal sign-off given it also means reduced safety coverage during that same outage.
- **Access control:** Pulse Radar console and Crisis Mode must be restricted to named, role-based accounts with mandatory two-person approval for Crisis Mode (FR-6); all actions logged to an immutable audit trail retained for 2 years. *(V1 recommended default.)* `[PM INPUT NEEDED: Legal]` Final retention period must be confirmed against India's Digital Personal Data Protection Act, 2023, alongside any other applicable regional requirements.
- **Security/Privacy:** Signal computation operates only on public content, its metadata, and public engagement/comment data; no private message content is in scope for V1.
- **Language coverage:** FR-2's intent classifier must cover Hindi and major regional Indian languages, not English alone, given the confirmed user base. `[PM INPUT NEEDED]` Exact language priority order for V1; ideally set by real usage-language distribution data.
- **Regional variance (India): CONFIRMED, no longer generic.** India's IT Amendment Rules, 2026 (effective Feb 20, 2026) compel a 3-hour takedown window on valid government notice (from an authorized officer, Deputy Inspector General of Police rank or above) for public-order and state-security content, with loss of safe-harbor protection for non-compliance. FR-5's 30-minute (Tier 3) and 10-minute (Tier 4-eligible) analyst SLAs are deliberately set well inside this statutory clock. `[PM INPUT NEEDED: Legal]` Exact mapping of the "public order" category to this PRD's mobilization-intent taxonomy (FR-2), and any state-level variation within India, still needs sign-off.

## 9. Success Metrics

- **Time-to-detection:** Median minutes from publication to first Tier 1+ flag for content later confirmed as genuinely mobilization-risk. **V1 launch target: < 10 minutes**, trending down release over release. *(Recommended default, not yet baselined.)*
- **Precision at Tier 3+:** % of Tier 3+ auto-routed cases upheld by human analysts. **V1 launch target: ≥ 70%**, rising to ≥ 85% within two quarters as the model recalibrates on real decisions.
- **Time-to-human-decision:** Median/P95 time from Tier 3+ flag to analyst decision. **V1 target: P50 < 15 min, P95 < 30 min**: met within the FR-5 SLA at least 95% of the time, and well inside India's 3-hour regulatory takedown deadline (§8).
- **Appeal overturn rate:** % of Tier 2+ actions overturned on appeal. **V1 target: < 15% sustained**: two consecutive weeks above 25% auto-triggers a mandatory review of the FR-4 combination table.
- **Crisis Mode activation quality:** % of activations later judged unnecessary in post-incident review. **V1 target: < 20%**: a proxy for whether the Tier 4 escalation bar is calibrated correctly.

## 10. Open Points

- **Validate, don't trust, the V1 defaults.** Every numeric threshold in this PRD (FR-1–FR-7, §8, §9) is a defensible starting recommendation; not empirically validated. Data Science + Policy must recalibrate all of them against real production data within the first 60 days.
- `[PM INPUT NEEDED]` Definition of "cohort baseline" for velocity anomaly (FR-1); exactly how creator-size tiers, sound clusters, and category cohorts are defined and refreshed is domain logic not fabricated here.
- `[ASSUMPTION – NEEDS VALIDATION]` Fail-open default during system outage (§8); the call is made and the rationale stated, but it still needs explicit Policy/Legal sign-off.
- **Hard dependency:** FR-3's coordination scoring needs a labeled historical dataset of known-organic vs. known-coordinated spread events. Does it exist today, or must it be built first? If built, that likely gates the V1 timeline; the biggest schedule risk in this PRD.
- **Scope decision to confirm:** Cross-platform coordination (a campaign seeded off-platform, imported to PulseReel) is explicitly out of scope for V1. Recommended: accept this boundary for V1 despite it being a known evasion path, since cross-platform signal ingestion would materially delay launch; but this is a leadership tradeoff to confirm, not mine alone.
- **Open question (narrowed, not generic anymore):** Now that India's IT Amendment Rules, 2026 confirm the general regulatory framework (§8), Legal still needs to map the "public order" category precisely onto FR-2's mobilization-intent taxonomy, confirm any state-level variation within India, and confirm DPDP Act, 2023 interaction for audit-log retention.
- **Open question:** Staffing model for 24/7 Pulse Radar coverage and Crisis Lead on-call rotation; the FR-5/FR-6 SLAs are only real if this is funded and staffed.
- **Open question:** Should Tier 1 (silent observation) ever be user-visible (e.g., a future transparency report), or stay purely internal? Leaning "internal only for V1, revisit for V2"; flagged, not decided, given PR/regulatory-disclosure implications beyond this PRD's scope.
- **Outstanding from PM (§4):** Actual creator appeal/support-ticket language has not yet been provided. Section 4's Creator mental model is not complete until real text is dropped in directly; it is deliberately not filled with invented placeholder quotes.
- **Outstanding from PM (§4):** Viewer mental model remains fully unconfirmed; no real research has been provided for this persona yet.
