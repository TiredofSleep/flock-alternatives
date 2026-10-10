# Transparency-by-design and audit-log governance

Research digest, Oct 9, 2026. **Through-line:** the cryptography is the easy part. The hard parts are identity, key custody, and the gap between "logged" and "reviewed." Every real deployment failed there.

## Tamper-evident logging
- Hash chain or Merkle tree: altering any entry breaks every hash after it. Merkle trees add inclusion proofs and consistency (append-only) proofs. ([DesignGurus](https://www.designgurus.io/answers/detail/how-do-you-design-tamperevident-audit-logs-merkle-trees-hashing))
- **Reference system: Google Trillian / Certificate Transparency.** Open source, Merkle-backed, signed tree heads, runs on MySQL. ([Trillian](https://google.github.io/trillian/))
- **Cautionary example: Amazon QLDB is retired** (end of support July 31, 2025). Don't hang integrity on one vendor's ledger product. ([InfoQ](https://www.infoq.com/news/2024/07/aws-kill-qldb))
- WORM / object-lock storage plus a hash chain is the regulator-blessed, small-shop-feasible approach (SEC 17a-4 pattern). ([dev.to](https://dev.to/veritaschain/building-cryptographic-audit-trails-for-sec-rule-17a-4-a-technical-deep-dive-4hbp))
- **Failure modes:**
  - Whoever holds the signing key can forge.
  - App-level append-only means nothing if the DBA has DELETE.
  - Split-view equivocation: showing auditors a different log than everyone else.
  - **Kill condition:** if no independent party ever pins or compares root hashes, the log is tamper-evident to nobody. The cheap fix is to publish the root hash somewhere public with a timestamp.
- NIST SP 800-92 (log management) and the NIST 800-53 AU control family are the compliance spine.

## Purpose-logged access already exists
- CJIS/NCIC/III already require per-transaction logging and purpose codes. ([Honolulu PD policy](https://honolulupd.org/policy/policy-security-of-data-from-the-ncic-interstate-identification-index))
- N-DEx: unique logins, annual access agreement, a purpose code on every search, audited every **3 years**. That's detection measured in years. ([Texas DPS](https://www.dps.texas.gov/administration/crime_records/training/ndex_overview_and_audit.pdf))
- CA SB 34 already requires an ALPR access log. ([text](https://atrn.assembly.ca.gov/sites/atrn.assembly.ca.gov/files/SB%2034%20%28Hill%29.pdf))
- **Flock's failures:**
  - 4,000+ ICE-related lookups (Danville IL logs, reasons literally "immigration", "ICE+ERO"). ([SAN/404](https://san.com/cc/ice-illegally-gains-informal-access-to-nationwide-license-plate-camera-network/))
  - A Texas officer's nationwide abortion search led Flock to pull IL, CA, and VA from National Lookup. ([404 Media](https://www.404media.co/flock-removes-states-from-national-lookup-tool-after-ice-and-abortion-searches-revealed/))
  - **A DEA agent used a local Palos Heights officer's password.** ([404 Media](https://www.404media.co/feds-used-local-cops-password-to-do-immigration-surveillance-with-flock-cameras/))
  - Detection always came from outside: FOIA, journalists, leaks.
- **CA State Auditor:** agencies did "little to no auditing" of ALPR searches, and one sheriff shared with 1,000+ entities in 44 states. A mandated log with zero review. ([EFF summary](https://www.eff.org/deeplinks/2020/02/california-auditor-releases-damning-report-about-law-enforcements-use-automated))

## Federated sharing networks: precedent and caution
- N-DEx has owner-controlled sharing, the most structured of the networks. LInX is MOU-governed, with no single accountable auditor. Fusion centers: a 2012 bipartisan Senate PSI report called the output "oftentimes shoddy," with civil-liberties infringements and mission creep. ([Senate PSI](https://www.hsgac.senate.gov/subcommittees/investigations/rep/investigative-report-criticizes-counterterrorism-reporting-waste-at-state-local-intelligence-fusion-centers/))
- **Lessons:**
  - Owner-controlled, opt-in per recipient, logged, and periodically re-justified.
  - Audit quality collapses to the weakest participant.
  - Name **one** body accountable for any audit that crosses a jurisdiction line.

## Dashboards that work
- Oakland's annual ALPR reports to its Privacy Advisory Commission. ([2020](https://www.oaklandca.gov/files/assets/city/v/1/boards-amp-commissions/documents/pac/automated-license-plate-reader-annual-report-2020.pdf))
- Seattle OIG ALPR usage review, an independent audit of actual query logs. ([PDF](https://www.seattle.gov/documents/departments/oig/audits/surveillancetechnologyusagereview-automatedlicenseplatereader-patrol(2021and2022).pdf)) This is the closest working model.

## Design requirements that fall out
1. An external party pins the root hash.
2. Enforced individual authentication, no shared accounts.
3. Validate the case number against real cases, not free text.
4. Funded log review on a cadence of days.
5. Publish sharing recipients and anomaly counts.
