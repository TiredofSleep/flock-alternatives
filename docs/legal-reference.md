# ALPR Legal Reference

**Clark County / Arkadelphia, Arkansas — county-owned license-plate-reader system**

Oct 9, 2026 · Prepared by @Brayden

This sheet summarizes the laws governing a county-owned automatic license plate reader (ALPR) system — one where Clark County or the City of Arkadelphia owns the hardware, software, and data, and every access runs through a single logged channel. It is a reference for the Sheriff, the Police Chief, and county counsel. It is not legal advice; it flags what the law already requires and what an authorizing ordinance would need to add.

## Arkansas ALPR statute

Arkansas regulates ALPRs under the Automatic License Plate Reader System Act, A.C.A. §§ 12-12-1801 to 1808, amended by [Act 668 of 2025 (SB 446)](https://www.ncsl.org/technology-and-communication/automated-license-plate-readers-state-statutes), effective August 5, 2025. The statute already encodes much of what a county-owned system needs.

- **Who may operate (§ 12-12-1803).** ALPR use is unlawful except for enumerated purposes — chief among them a state, county, or municipal law-enforcement agency comparing data for a legitimate law-enforcement purpose. Private landowners and businesses may use ALPRs on their own property. The default is prohibition; lawful use is the exception.
- **Retention (§ 12-12-1804).** Captured plate data may be kept no more than 150 days by government users (60 days for private users), except data tied to an ongoing investigation, which is destroyed when the case closes without charges or otherwise concludes.
- **No sale or sharing.** A government entity shall not sell, trade, or exchange captured plate data, and may compel data held by a private user only by valid subpoena. Public disclosure is limited to the registered owner with written consent, or as federal law allows.
- **Audit, statistics, and published policy (§ 12-12-1805).** A government user must compile semiannual statistics (scans, lists checked, matches, arrests, prosecutions), keep them 18 months, and adopt and publish its obtain/retain/destroy policy. A court may exclude evidence obtained in violation of the subchapter where the required policy is not published.
- **Evidence bar (§ 12-12-1806).** Evidence whose disclosure would violate the subchapter is barred.
- **Private right of action (§ 12-12-1807).** A person harmed may recover actual damages or $1,000 liquidated damages, whichever is greater; the Attorney General may also sue under the Deceptive Trade Practices Act.

## Operator of record: CJIS & ACIC

Reading plates is not the regulated part — matching them against criminal-justice databases is. Keeping that line clear is what keeps a county system out of full federal accreditation.

- **Where CJIS applies.** Plate capture plus a locally-held hotlist is not governed by the FBI Criminal Justice Information Services (CJIS) Security Policy. CJIS applies the moment reads are crossed against NCIC (national) or ACIC (Arkansas) wanted or stolen data.
- **Use the ACIC channel.** Small Arkansas agencies typically operate under ACIC Indirect Access — hotlist hits come through a dispatch center or a parent agency that already has a terminal, rather than a new pipe the county builds and must accredit itself. Confirm the workflow with ACIC before buying hardware.
- **What CJIS requires if the system touches that data.** Multi-factor authentication, encryption in transit and at rest, audited access with actual periodic review, and fingerprint-based background screening for everyone who touches the data — including IT staff and outside vendors. A felony conviction bars access, and any non-criminal-justice vendor needs a CJIS Security Addendum pre-approved by ACIC.

## Fourth Amendment status

A county cannot rely on the Fourth Amendment to suppress misused ALPR data — the law runs the other way. The enforceable lever is the Arkansas statute above, written into the ordinance below.

- **General rule: no warrant.** Courts hold there is no reasonable expectation of privacy in a plate displayed in public or in movements on public roads (United States v. Knotts, 1983; the third-party doctrine). Most ALPR queries are not treated as a search.
- **The mosaic exception is narrow and unsettled.** Carpenter v. United States (2018) suggested comprehensive, long-term tracking can become a search. Applied to ALPR mainly at the state level — Commonwealth v. McCarthy (Mass. 2020) held dense, dragnet ALPR tracking could require a warrant, but still admitted the evidence because the surveillance there was too limited.
- **Recent decisions favor admission.** United States v. Porter (5th Cir. 2026) held an ALPR query is not a search; United States v. Martin (E.D. Va. 2024) denied an ALPR suppression motion; Schmidt v. City of Norfolk (E.D. Va. 2026) upheld a 170-camera network (“not today”), now on appeal.
- **Bottom line.** No reported case has suppressed ALPR evidence on Fourth Amendment grounds, or treated a missing log entry as the trigger. The log’s legal value is to make misuse provable — powering the § 12-12-1807 claim and the ordinance remedy — and to make evidence that did pass through the logged door defensible in court.

## What the county ordinance must encode

To make the design legally real, the authorizing ordinance should convert the statute’s defaults into binding, enforceable commitments:

1. **Default-illegal use**, mirroring § 12-12-1803, with the permitted law-enforcement purposes named.
2. **One logged front door** — every access authenticated to an individual, no shared accounts, no outside standing logins, and no national-lookup feature built at all.
3. **Express exclusion clause** — evidence obtained through unlogged or unauthorized access is inadmissible, bolted onto the §§ 12-12-1805 and 1806 hooks.
4. **Automatic retention deletion** at the statutory cap, enforced in software rather than by hand.
5. **No external sharing** except through a logged lawful request — warrant, court order, or statutory hotlist match — each recorded with a case number.
6. **One named auditor** outside the searching unit, with a published review on a short cadence — the control every documented ALPR failure has lacked.
7. **Tamper-evident log** whose current state is pinned by an outside witness (county clerk or equivalent), so the record cannot be quietly rewritten.
8. **Public reporting** beyond vehicle counts — including sharing recipients and query volumes — consistent with the § 12-12-1805 semiannual report.

## Federal procurement & pilot legality

- **Federal procurement (verify first).** NDAA Section 889 bars Hikvision and Dahua equipment for federal agencies and federally funded purchases. If any federal grant money touches the project, those cameras are off the table — confirm the current rule and the funding source before buying.
- **Private-property pilot.** A business owner may lawfully run an ALPR on their own property under § 12-12-1803, subject to the 60-day retention cap. A camera at a private lot is a legal way to prove the system works before any public deployment.

## Sources

- Arkansas Code §§ 12-12-1801 to 1808 — Automatic License Plate Reader System Act, as amended by Act 668 of 2025 (SB 446)
- [NCSL — Automated License Plate Readers: state statutes](https://www.ncsl.org/technology-and-communication/automated-license-plate-readers-state-statutes)
- Carpenter v. United States, 585 U.S. 296 (2018)
- Commonwealth v. McCarthy, 484 Mass. 493 (2020)
- United States v. Porter (5th Cir. 2026); United States v. Martin (E.D. Va. 2024); Schmidt v. City of Norfolk (E.D. Va. 2026)
- FBI CJIS Security Policy; Arkansas Crime Information Center (ACIC) Indirect Access

---

*This is a plain-language summary of a genuinely unsettled area of law, provided for reference only. It is not legal advice and creates no attorney–client relationship. Statutory text and case law change; verify the current Arkansas Code and have a licensed Arkansas attorney draft the authorizing ordinance before relying on any of it.*
