# Prior art: community-controlled and locally-owned surveillance

Research digest, Oct 9, 2026. **Bottom line:** the governance models are mature and can be copied. Self-hosted ownership of an ALPR system is essentially greenfield; nobody does it.

## CCOPS (ACLU "Community Control Over Police Surveillance")
- Model ordinance requirements: a surveillance impact report and use policy published before acquisition, public notice and comment, council approval of both, annual reports, and approval revisited at least yearly. Existing tech must win approval or be discontinued. Around 21 jurisdictions had adopted it as of 2021. ([ACLU](https://www.aclu.org/news/criminal-law-reform/the-people-not-the-police-should-decide-if-and-how-surveillance-technologies-are-used-in-their-communities), [EFF](https://www.eff.org/deeplinks/2021/05/community-control-police-spy-tech))
- **Santa Clara County (2016):** the first one, and the template.
- **Oakland:** the strongest. Approval requires findings that benefits outweigh costs and that no cheaper alternative exists. A standing Privacy Advisory Commission reviews proposals, and non-disclosure agreements are banned. ([EFF](https://www.eff.org/deeplinks/2018/05/oakland-new-gold-standard-community-control-police-surveillance))
- **Seattle:** public Master List of surveillance tech, plus Office of Inspector General review of actual usage.
- **Somerville, MA:** evidence collected in violation is **excluded from court**. This is the tooth worth copying.
- **Boston and Lawrence, MA:** private right of action and employee discipline. **Davis, CA:** attorney's fees for prevailing plaintiffs.
- **Cautionary example, NYC POST Act:** disclosure only. It surfaced about $3B in hidden NYPD contracts, but the NYPD routinely ignores it. Without teeth, it's theater. ([EFF](https://www.eff.org/deeplinks/2023/11/stop-putting-check-unchecked-local-ny-government-surveillance))

## Oakland Domain Awareness Center (the canonical scale-back)
- 2013: a planned citywide fusion center tying together 700+ cameras, facial recognition, ALPR, and 300 TB of data. After public pushback, the council in 2014 limited it to the Port only and banned facial recognition and ALPR. A citizen committee became the permanent Privacy Advisory Commission. **Lesson: the win was institutional. A standing independent body outlived the fight.** ([ACLU NorCal](https://www.aclunorcal.org/news/hofer/))

## The Flock exodus (2025–26)
- Secure Justice counts **214 jurisdictions** that dropped Flock since 2021, **90 of them in Aug 2026**. ([Cybernews](https://cybernews.com/privacy/flock-cameras-us-cities-record-terminations/))
- Named examples: El Cerrito CA (federal access concerns), Appleton WI, Bloomington IN, Tompkins County / Ithaca / Saranac Lake NY, Menominee MI (activated without council approval), and Ypsilanti MI (banned ALPR outright). ([Newsweek](https://www.newsweek.com/map-cities-rejected-deactivated-flock-cameras-12253499))
- **Replacements were all other vendors, not local ownership.** Bernalillo County NM moved to Axon, citing county-controlled data, no national pooling, sharing off by default and revocable, role-based access, and audit logs with reasons. That's effectively our spec, but rented. ([KRQE](https://www.krqe.com/news/albuquerque-metro/bernalillo-county-sheriffs-office-transitions-to-axon-automatic-license-plate-readers/amp/)) Dane County WI is also doing a vendor swap.
- **What made Flock radioactive:** 404 Media's reporting on local PDs running lookups for ICE, and a Texas officer's nationwide search for a woman who self-managed an abortion. Separately, a WaPo report found 46+ officers accused of using Flock to stalk women.

## Transparency portals
- Flock "Transparency Portals" (Milwaukee, Columbia County NY, Oakland) show only aggregates. They don't show per-search reasons, who searched, or sharing recipients. Detailed logs come out only through records requests. ([Milwaukee](https://urbanmilwaukee.com/pressrelease/mpd-launches-flock-alpr-transparency-portal/))
- Lexington KY voluntarily publishes quarterly Flock audit memos, which is rare. ([PDF](https://lexingtonky.gov/sites/default/files/2024-08/Q2%202024%20FLOCK%20AUDIT.pdf))
- **The reason-field scandal:** "idk," "LMAO," "asdfg," "TBD" across 30+ agencies. One Goshen IN "idk" search hit 82,413 cameras, and there were 6,300+ "TBD" searches. Flock's dropdown fix was called "a loss for transparency" by EFF. ([State of Surveillance](https://stateofsurveillance.org/news/flock-alpr-audit-logs-lmao-asdfg-reason-field-2026/))

## Civil-society resources
- ACLU (CCOPS model bill), EFF (Atlas of Surveillance, Street Level Surveillance), Oakland Privacy (helps draft ordinances), S.T.O.P. (NYC), DeFlock (camera map and tracker of the exodus), and Secure Justice (cancellation count).
