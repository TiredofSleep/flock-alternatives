# ALPR Action Plan

Oct 9, 2026 · @Brayden

The plan runs from the meeting with Sheriff Jason and Chief Jackson to a county-owned pilot, with one hard gate: nothing gets built until ACIC confirms how hotlist access works and the Quorum Court passes the ordinance.

## 1. Before the meeting

Walk in with one ask, the facts cold, and ideally a camera already reading plates.

- [ ] Pick the lead ask: a small county-owned pilot the sheriff owns and can shut off
- [ ] Re-read the Meeting Brief: the two objections (“who fixes it at 2am” and “Flock tells us about stolen cars from Little Rock”) and their answers
- [ ] Call ACIC at (501) 682-2222 as a private developer, general questions only, and note any names and document titles they give
- [ ] Look up the Arkadelphia Flock grant end date (the 2024 Ross Foundation grant covered install plus two years) so you know if renewal is live
- [ ] If time allows: stand up Frigate and one LPR camera at the Arkadelphia Ozark lot, so “come see it running” is true
- [ ] Print two copies of the ALPR Legal Reference to bring

## 2. The meeting with the two Jasons

The goal is one small yes from the sheriff: the name of the staff member who handles ACIC. Everything else is setup for that ask.

1. **Open by defusing.** “I’m not here to tell anyone to pull anything out. I build software, I live here, and I want to show you an option.” Chief Jackson keeps his Flock; don’t make him defend it.
2. **State the thesis.** With Flock you trust a company’s word about your town’s data. With a county-owned system, every search goes through one logged door, and someone outside the department can check the log.
3. **Show the law is already on your side.** Act 668 already makes non-enumerated use illegal, bans selling data, caps retention at 150 days, and requires public reports. The county ordinance adds teeth.
4. **Be straight about the hard parts.** CJIS/ACIC and long-term maintenance. Say you know they’re the hard part and you’re working the ACIC side first.
5. **Make the ask.** A 2–3 camera pilot the county owns.
6. **Close with the small yes.** “The first real question is how ACIC handles hotlist access. Who on your staff handles ACIC? I’d like to call them together.”

After the meeting, write down what each Jason said, any objections, and the name you got.

## 3. First two weeks after

The joint ACIC call decides which version of this project exists.

- [ ] Within 24 hours: thank-you email to both Jasons restating the one next step
- [ ] Schedule the joint call with the sheriff’s ACIC person (likely his Terminal Agency Coordinator)
- [ ] On the call, ask how LPR systems in Arkansas receive hotlist data, what agreement it takes, and whether a county server holding the hotlist becomes a CJIS system
- [ ] Write up what ACIC said and send it to the sheriff

**Decision gate after the call:**

| ACIC answer | What it means | Next move |
| --- | --- | --- |
| Hotlist available to agency-approved systems; matching can run on the agency side | Your build is plate capture plus a local log; CJIS exposure is small | Go to policy (section 4) |
| A county server holding the hotlist becomes a CJIS system | Doable, but needs a CJIS IT audit and a sheriff-controlled network | Price the audit, then policy |
| Only state-approved vendors | You need vendor approval first | Ask how a vendor gets approved; pause the pilot until then |

## 4. Policy before cameras

Write the rules first so the software enforces real law, not guesses. The sheriff can champion this, but the County Judge and Quorum Court pass ordinances and appropriate money.

- [ ] Ask the sheriff to bring in county counsel to draft the ordinance
- [ ] Draft from the CCOPS model plus Arkansas §§ 12-12-1803 to 1807: one logged door, exclusion clause, auto-delete at the cap, no outside sharing without a logged lawful request, one named outside auditor, external witness on the log, public reports
- [ ] Brief the County Judge before it goes to the Quorum Court
- [ ] Line up pilot funding; the Ross Foundation funded Arkadelphia’s Flock grant, so ask whether they’d fund a county-owned pilot
- [ ] Quorum Court vote on the ordinance and the pilot appropriation
- [ ] You: complete fingerprint check, CJIS security training, and sign the FBI Security Addendum

## 5. Pilot

Two to three cameras on one county chokepoint, run for 90 days, to prove every promise before anyone scales it.

| Must prove | How you show it |
| --- | --- |
| Plates read at road speed | Read-rate report against a hand-checked sample |
| Every search is logged with a person and a case number | Sample audit of the log; no search without a case number |
| The log can’t be quietly edited | Outside witness pins the log’s hash on a schedule; one verification demo |
| No shared accounts | Individual logins with MFA for every user |
| Data deletes on schedule | Retention report showing nothing older than the cap |
| Hotlist alerts reach deputies | Count of alerts and how they were handled |

End with a public report to the Quorum Court, including any misreads and failures.

## 6. Scale and staffing

Don’t expand past the pilot until someone besides you can keep it running.

- [ ] A named, fingerprint-cleared person (county IT or a contracted support arrangement) owns patching and uptime
- [ ] Written runbook so the system survives you leaving
- [ ] Annual budget line for LTE, storage, and replacements
- [ ] Code published as open source so the county is never locked to you
- [ ] Then add cameras, and offer the same setup to Arkadelphia when its Flock renewal comes up

## 7. Open questions

- When is the meeting with the two Jasons?
- When does Arkadelphia’s Flock grant run out, and what does renewal cost?
- Is this a paid contract for you, a donation, or something in between? Decide before the sheriff asks.
- Who would be the outside auditor: a citizen board, the county clerk, or someone else?
- Will any federal grant money be involved? If so, Hikvision and Dahua cameras are off the table under NDAA Section 889.
