# Clark County ALPR — project context

Brayden Sanders (7Site LLC, Hot Springs AR; owner of Ozark Cleaners in Hot Springs and Arkadelphia) is working to get Clark County, Arkansas to own its own license-plate-reader (ALPR) system instead of renting one from Flock Safety. He builds software (CustomPOS) and is pitching this as a local, county-owned, open-source system.

This folder is the handoff from a research/planning session. Read `HANDOFF.md` for current status and next tasks.

## The thesis (settled — don't relitigate)

We can't keep federal agencies or anyone else out. Data crosses networks and the feds have lawful means. So the system doesn't promise secrecy. It promises **knowability**:

- **One logged front door.** Every access is authenticated to one individual, has a stated reason tied to a real case number, and is recorded in a tamper-evident log.
- **Every other door is illegal.** The county ordinance makes any access outside the front door punishable misconduct for local personnel. (A local ordinance can't bind federal agents. It binds the county's own system and people.)
- **Someone outside the department can check the log.** An external witness pins the log's hash. A named outside auditor reviews it on a short cadence. Public reports include sharing recipients and query volumes, not just vehicle counts.

The pitch line: "With Flock, you trust a company's word about what happens to your town's data. With this, you can check."

## Hard constraints and corrections

- **Don't oversell suppression.** The Fourth Amendment path is weak. *U.S. v. Porter* (5th Cir. 2026) held that an ALPR query is not a search. No reported case has suppressed ALPR evidence on constitutional grounds or treated a missing log entry as the trigger. The real enforcement spine is **Arkansas statute**: A.C.A. §§ 12-12-1801–1808 as amended by Act 668 of 2025. Use is unlawful except for enumerated purposes. Retention is capped at 150 days (60 for private). Sale, trade, or exchange of data is barred. § 1805 has an exclusion hook, § 1806 is an evidence bar, and § 1807 gives a private right of action with $1,000 liquidated damages. The ordinance adds an express exclusion clause on top of these.
- **Keep NCIC/ACIC hotlist matching on the ACIC side** if at all possible. Plate capture plus a local log is not CJIS-regulated. Crossing reads against NCIC/ACIC data is. This one boundary decides whether the build needs a full CJIS IT audit. It is unconfirmed until the ACIC call.
- **Every pillar fails on review, never on crypto.** The documented failures are all governance failures:
  - Flock's free-text reason fields filled with "idk" and "LMAO."
  - A DEA agent searched under a local officer's password.
  - California agencies had a logging law and never reviewed the logs.

  Design each pillar together with the control that prevents its known failure (see `design/architecture.md`).
- **Don't architect around OpenALPR.** It's been dead since 2018. Use Frigate NVR (YOLOv9 plus PaddleOCR) or fast-alpr (MIT). Platerecognizer self-hosted is the paid fallback.
- **Shutter speed reads plates, not megapixels.** You need 1/1000s minimum (1/2000s at night or speed), IR, and about 100 pixels per foot on the plate. Use motorized varifocal lenses for road speed.
- **NDAA §889:** if any federal money is involved, Hikvision and Dahua are out. Verify before buying.
- **Maintenance is the real risk.** The project dies at year 3 if there's no named, fingerprint-cleared owner for patching and uptime. Don't scale past the pilot without that.

## People and politics

- **Chief Jason "Shorty" Jackson, Arkadelphia PD.** Bought Flock in 2024 on a $30,750 Ross Foundation grant covering install plus 2 years. Publicly committed ("here to stay"). He is not the buyer. Never make him defend Flock.
- **Sheriff Jason, Clark County.** Has no ALPR system. He's the actual customer.
- **County Judge and Quorum Court** pass ordinances and appropriate money. The sheriff can champion this but can't approve it alone.
- **Ross Foundation** is a possible pilot funder.
- Brayden emailed the sheriff the Legal Reference PDF on Oct 9, 2026 ("Flock alternatives — here's what I've turned up in research so far"). The meeting with both Jasons is set; the date is TBD.

## Working with Brayden

He's direct, analytically rigorous, and darkly funny. Match that. Keep kill-condition honesty: name how each idea fails, and don't validate claims the evidence doesn't support. Never tell him to rest or take a break.

## Folder map

- `HANDOFF.md`: status, decisions, prioritized next tasks
- `docs/`: deliverables already made
  - `meeting-brief.html`: what to say in the room
  - `blueprint.html`: the build-it-real strategy plus kill-conditions
  - `legal-reference.md` and `.pdf`: what was emailed to the sheriff
  - `action-plan.md`: phased checklist
- `design/architecture.md`: system design spec for the software
- `research/`: sourced research digests (governance, audit logs, case law, build path/CJIS, ACIC call prep)
