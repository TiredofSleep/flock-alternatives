# ALPR and the Fourth Amendment / suppression: current status

Research digest, Oct 9, 2026. A summary with citations, not legal advice.

**Bottom line:** the argument that a "logged front door makes unlogged access suppressible" is **weak under the Fourth Amendment** and **moderately stronger under the Arkansas statute**. No reported case uses the absence of a log entry as a suppression trigger.

## Carpenter and the mosaic theory
- *Carpenter v. U.S.*, 585 U.S. 296 (2018) carved a narrow exception covering 7 days of historical cell-site location data. It did not adopt the mosaic theory wholesale.
- *Commonwealth v. McCarthy*, 484 Mass. 493 (2020) is the leading pro-defendant case: dense, dragnet ALPR **could** be a search. But 4 cameras at 2 bridges was too limited, so the evidence came in. Gants' concurrence proposed preserving query records for discovery. ([HLR](https://harvardlawreview.org/print/vol-134/commonwealth-v-mccarthy/), [opinion](https://www.eff.org/files/2020/05/05/mccarthy-sjc-12750_07_opinion.pdf))
- *U.S. v. Porter*, 170 F.4th 381 (5th Cir. 2026): an ALPR query is **not a search**. No warrant required. ([analysis](https://dlglearningcenter.com/?p=108098))
- *Leaders of a Beautiful Struggle v. Baltimore PD*, 2 F.4th 330 (4th Cir. 2021, en banc): city-wide aerial surveillance violated the Fourth Amendment. Analogous, not ALPR.
- *People v. Tafoya*, 494 P.3d 613 (Colo. 2021): 3+ months of pole-camera surveillance of a home was a search. Analogous.
- Orin Kerr argues the mosaic theory is unworkable. ([Volokh](https://reason.com/volokh/2020/04/22/automated-license-plate-readers-the-mosaic-theory-and-the-fourth-amendment/printer/))

## Majority position: no warrant
- *U.S. v. Knotts* (1983): no reasonable expectation of privacy in movements on public roads.
- *U.S. v. Martin* (E.D. Va. 2024): Flock ALPR suppression **denied**. ([VLW](https://valawyersweekly.com/2024/10/28/search-and-seizure-motion-to-suppress-license-plate-reader-evidence-denied/))
- *Schmidt v. City of Norfolk* (E.D. Va. Jan 2026): 170+ Flock cameras upheld, "not today." Appeal to the 4th Circuit likely. ([WHRO](https://whro.org/business-growth/2026-02-11/a-federal-judge-ruled-norfolks-flock-surveillance-cameras-dont-invade-peoples-privacy-yet))
- CRS survey: no federal appellate court has held an ALPR query is a search. ([CRS](https://www.everycrsreport.com/files/2025-07-21_IF13068_c5195bc8a2eeae98e20886a014066705ea674de7.html))

## Why suppression rarely happens
1. No search means no violation, so there's nothing to exclude.
2. The good-faith exception (*Leon*, *Krull*, *Davis*) usually saves evidence while the law is unsettled.
3. The exclusionary rule is a Fourth Amendment remedy. Violating a policy or statute doesn't trigger it unless the statute itself provides exclusion.

## State law
- About 28 states have ALPR statutes. Retention runs from 3 minutes (NH) to 5 years (AL), typically 21–90 days. Warrant requirements are narrow (NJ sharing, CT some sharing, MN tracking); none requires a blanket warrant to query. ([NCSL](https://www.ncsl.org/technology-and-communication/automated-license-plate-readers-state-statutes))
- Audit-log mandates exist in VA (2-year audit-trail retention; misuse is a Class 1 misdemeanor), AL, ID, MT, NH, and CA. These create accountability, not suppression.

## Arkansas: the actual spine
A.C.A. §§ 12-12-1801–1808, as amended by Act 668 of 2025 (SB 446), effective Aug 5, 2025. ([summary](https://www.recordinglaw.com/us-laws/automated-license-plate-readers/arkansas-alpr-laws/), [EFF](https://eff.org/ALPRstatelaws))
- **§1803:** unlawful except for enumerated uses (law-enforcement comparison, parking, secured-area access, private owners on their own property, Highway Police).
- **§1804:** retention capped at 150 days for government, 60 for private. Investigation data is destroyed when the case closes or concludes.
- Government shall not sell, trade, or exchange data. Private data can be compelled only by subpoena.
- **§1805:** semiannual stats kept 18 months, plus a published policy. **A court may exclude evidence if the required policy isn't published.**
- **§1806:** bars evidence whose disclosure would violate the subchapter.
- **§1807:** private right of action, the greater of actual damages or $1,000 liquidated. The AG can sue under DTPA.
- No Arkansas appellate decision has construed the Act yet.

**The move:** write an express exclusion clause for unlogged access, plus an audit-trail retention mandate, into the county ordinance, on top of §§1805–1807. The log's job is to make misuse provable and clean evidence defensible.
