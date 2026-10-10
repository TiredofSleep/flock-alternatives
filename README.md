# Flock alternatives: a research hub

> **Status: research and planning, not a product.** Everything here is a working file from an ongoing
> effort in **Clark County, Arkansas**. It's published as-is so other towns and counties can use it.
> It is not legal advice. Verify every claim against its source before relying on it.

Hundreds of jurisdictions have dropped or paused Flock Safety's license-plate cameras since 2021,
mostly over who else can search the data (`research/01-governance-prior-art.md`). Most replaced
Flock with another vendor. This hub lays out **every option we found**, including one almost nobody
has tried: **a county that owns its own system, where every search goes through one logged door that
someone outside the department can check.**

> "With Flock, you trust a company's word about what happens to your town's data. With this, you can check."

---

## The options

| option | what it is | trade-offs | where to read |
|---|---|---|---|
| **Stay with Flock, add oversight** | keep the cameras; pass an ordinance that sets the rules | cheapest change; data stays in Flock's cloud and national network | `research/01-governance-prior-art.md` |
| **Switch to a vendor with local storage** | Rekor (local install and processing), Leonardo/ELSAG (local hardware), Axon (local storage option, sharing off by default) | proven, supported; still rented. Bernalillo County NM moved to Axon on these terms | `research/04-build-path-cjis.md` |
| **County-owned, open source** | commodity LPR cameras + Frigate NVR or fast-alpr on county hardware, with a logged front door, outside witnesses and public reports | the county owns the data and the code; needs a named local maintainer and CJIS diligence | `design/architecture.md`, [civic-lightlog](https://github.com/TiredofSleep/civic-lightlog) |
| **Hybrid** | a vendor's cameras feeding county-owned storage and audit logging | less to build; depends on the vendor allowing it | `research/04-build-path-cjis.md` |
| **No ALPR** | some cities banned it outright (e.g. Ypsilanti MI) | no data to misuse; loses stolen-vehicle and Amber-alert hits | `research/01-governance-prior-art.md` |

**Whichever option a community picks, the governance is the part that protects people:** a
Community Control Over Police Surveillance (CCOPS)-style ordinance, an exclusion clause for evidence
gathered outside the rules, one named outside auditor reviewing the logs on a short cadence, and
public reports that include who the data was shared with. Every documented abuse was a people and
oversight failure, not a technology failure.

### Rough cost comparison (from `research/04-build-path-cjis.md`; estimates, verify locally)
| | Flock | self-hosted |
|---|---|---|
| per camera | ~$2,500–3,000/yr + ~$250–350 install | ~$300–500 one-time |
| 6–10 cameras | ~$20–30k/yr | ~$15–40k one-time + server |
| ongoing | included | LTE, storage, replacements, and **staff time** (the real cost) |

---

## What's here

| path | contents |
|---|---|
| `docs/legal-reference.md` (+ `.pdf`) | Arkansas ALPR law (A.C.A. §§ 12-12-1801–1808, Act 668 of 2025), CJIS/ACIC, and what an ordinance should add |
| `docs/action-plan.md` | the phased plan from a first meeting to a county-owned pilot |
| `docs/meeting-brief.html`, `docs/blueprint.html` | meeting talking points; the build strategy with kill conditions (open in a browser) |
| `research/01-governance-prior-art.md` | CCOPS ordinances, Oakland, Seattle, Somerville; the Flock exodus; transparency portals |
| `research/02-audit-log-models.md` | tamper-evident logging, purpose-logged access, why mandated logs went unreviewed |
| `research/03-alpr-case-law.md` | the case law, and why Arkansas statute is the real enforcement spine |
| `research/04-build-path-cjis.md` | software, cameras, CJIS and ACIC, vendors, cost, maintenance risk |
| `research/05-acic-call-prep.md` | questions for the Arkansas Crime Information Center |
| `design/architecture.md` | the county-owned design: one logged front door and the control for each known failure |
| `design/sentinels.md` | one-way sentinel agents on every machine: forward-secure signed checkpoints to an outside witness, silence as the alarm, canary records |
| `design/ceremony-protocol.md` | the key ceremony, modeled on ICANN's root key ceremony and scaled to a county: separated roles, 3-of-5 cards across five institutions, two safes, a clean offline laptop, livestreamed |
| `design/ceremony-clerk.md` | an optional offline AI clerk for the ceremony: tools that return receipts only, a deterministic gate, and kill conditions set before testing |
| `HANDOFF.md`, `HANDOFF-UPDATE-2.md`, `CLAUDE.md` | working notes and task lists for continuing the work |

## Related
- **[civic-lightlog](https://github.com/TiredofSleep/civic-lightlog):** the open prototype of the
  logged front door, watchdog rules, commit-before-release receipts and sentinels (immature).
- Civil-society resources: ACLU (CCOPS model bill), EFF (Atlas of Surveillance), Oakland Privacy,
  DeFlock, Secure Justice.

## Use and contribute
Documents under CC BY 4.0: use and adapt them for your own community, with attribution. Corrections
with sources are welcome as issues or pull requests.

Brayden Sanders · Clark County, Arkansas
