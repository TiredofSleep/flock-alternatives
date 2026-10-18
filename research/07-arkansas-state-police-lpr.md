# Arkansas precedent: the State Police's own plate-reader system

Research digest, Oct 17, 2026. **Bottom line:** Arkansas already has a government-owned plate-reader
system running under published rules: the Arkansas State Police (ASP). It's the closest in-state
precedent for a county-owned system, and a likely partner on the hotlist side.

## What the ASP rules say (130.01.24 Ark. Code R. 002, "License Plate Readers Rules")
Source: [Cornell LII copy of the rule](https://www.law.cornell.edu/regulations/arkansas/130-01-24-Ark-Code-R-002);
the rules were also presented to the legislature ([arkleg.state.ar.us PDF](https://arkleg.state.ar.us/Home/FTPDocument?path=%2FAssembly%2FMeeting+Attachments%2F040%2F26607%2FD.14.a+DPS+ASP+Rules+for+License+Plate+Readers.pdf)).

| topic | ASP rule |
|---|---|
| **Ownership** | the LPR systems, equipment, databases and data are "the property of the Arkansas State Police" (Rule 5(d)) |
| **Who runs it** | the Interstate Criminal Patrol Commanders serve as the LPR Administrator (Rule 5(e)) |
| **Allowed use** | legitimate law-enforcement purposes only; excludes personal or professional gain, political purposes, and helping a member in a legal proceeding (Rules 4(g), 5(a), 6(b)) |
| **Before a stop on a hit** | the officer must visually confirm the plate and state, check it through dispatch or ACIC/NCIC, and try to confirm occupants match any wanted-person description (Rule 6(a)) |
| **Storage and retention** | on the designated LPR server, no more than 150 days (Rule 6(d)); data kept longer under A.C.A. § 12-12-1804(b) is deleted when no longer needed, **and the deletion is logged** (Rule 6(e)) |
| **Sharing** | only as A.C.A. § 12-12-1803 allows; **every disclosure goes in a dissemination log** (Rules 6(b), 6(c)) |
| **Query logs** | "LPR Data Query Logs" are defined (Rule 4(h)), but the rules don't specify their contents or a review schedule |
| **Reporting** | usage reports and results to the **Arkansas Legislative Council quarterly** (Rule 5(e)); statistics compiled for public review and kept 18 months (Rule 5(f)) |
| **Penalties** | misuse is punishable under A.C.A. §§ 12-12-212 and 12-12-1807 (Rules 5(b), 5(c)) |

## What it means for a county-owned system
- **It shows government ownership works in Arkansas.** "Can a public agency own its own plate readers
  and data?" already has a state-level yes, with published rules.
- **Its rules are a strong starting template.** The county ordinance and use policy can mirror ASP's
  structure (purpose limits, verification before a stop, deletion logs, dissemination logs, reporting).
- **Where the county design goes further:** ASP defines query logs but doesn't require what they
  contain or how often they're reviewed. The county plan adds a case-number check on every search, a
  named outside auditor on a short review cadence, an outside witness on the log, and public reports
  that name sharing recipients (`design/architecture.md`). Those are the controls every documented
  abuse in `research/02-audit-log-models.md` lacked.
- **A possible partner on the CJIS side.** The plan prefers keeping NCIC/ACIC hotlist matching on the
  state side. How ASP's system receives hotlists is a good question for the ACIC call
  (`research/05-acic-call-prep.md`).
- **Sharing:** ASP is already on the draft sharing allowlist in civic-lightlog's `rules.json`.

## Wider Arkansas context (2026)
- Flock is used by at least 39 Arkansas agencies per the Atlas of Surveillance, including Little Rock
  and Fort Smith ([Arkansas Times](https://arktimes.com/arkansas-blog/2026/01/12/little-rock-police-track-you-with-116-license-plate-readers-citywide-we-mapped-them-all)).
- Since July 2026, at least seven Arkansas cities announced they'd stop using Flock, including Searcy,
  Cabot, Mayflower, Greers Ferry, Centerton, Farmington and Pea Ridge; in August the Arkansas
  Association of Chiefs of Police publicly backed "lawful, ethical, accountable, and transparent use"
  of Flock ([NWA Democrat-Gazette](https://www.nwaonline.com/news/2026/aug/28/arkansas-police-chiefs-association-endorses-use/)).
- The Arkansas State Highway Commission proposed its own License Plate Reader Rules in April 2026
  (comments closed May 14, 2026) ([ArDOT notice](https://ardot.gov/news/26-048/)).
- March 2026: a family was stopped at gunpoint after a Flock camera apparently misread a plate
  ([Carscoops](https://www.carscoops.com/2026/03/alpr-camera-police-stop-arkansas/)). ASP's
  verify-before-stop rule (6(a)) is the control for exactly this.

## Open questions
- **Who supplies ASP's cameras and software?** Not found in public sources. Ask on the ACIC call, or
  file an Arkansas FOIA request for ASP's LPR contracts and its quarterly reports to the Legislative
  Council.
- **Do the quarterly reports to the Legislative Council include query counts and sharing recipients?**
  Request copies; they're a model (or a gap) for the county's public reports.
- **Would ASP share hotlist matching with a county system,** so the county box never holds CJIS data?
- **Has the Highway Commission rule been finalized,** and does it create a second state system?
