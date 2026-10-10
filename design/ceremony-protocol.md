# Ceremony protocol: the layers

Status: a design spec modeled on the ICANN/IANA Root Zone KSK ceremony, scaled to Clark County. Nothing is built. Pairs with `ceremony-clerk.md`, where the LLM is an advisory clerk inside this protocol.

References:
- [IANA Key Ceremony Roles](https://iana.org/help/key-ceremony-roles)
- [KSK Key Management Procedure v3.7](https://Iana.org/dnssec/procedures/ksk-operator/KSK_Key_Management_Procedure_v3.7.pdf)
- [APNIC: DNS security and key ceremonies](https://blog.apnic.net/2021/10/12/dns-security-and-key-ceremonies/)

## Principle

Thickness comes from **independent layers that fail differently**: different people, different institutions, physical custody, scripted procedure, and public recording. Corrupting one layer must not corrupt another. More machinery inside one layer is not thickness (Kerckhoffs). The cost of thickness is **people and time**, so ceremonies are rare. All the thickness lives in the ceremony, not in daily operations.

**When a ceremony happens:** at initial install (pinning each sentinel's starting key), at each software release signing, at key retirement or replacement, and after any suspected compromise. Expect 1–3 a year.

---

## Layer 1: Roles, with no person holding two

| Role | Who (county mapping) | Job |
|---|---|---|
| Ceremony Administrator (CA) | Designated by the county, not the system's builder | Reads the script aloud and performs most steps |
| Internal Witness (IW) | County Clerk's office | Checks the CA against the script, timestamps each step, writes exception reports. **The IW's signed record is the authoritative transcript.** |
| CA2 / IW2 | Backups from the same offices | Keep dual occupancy, escort attendees, substitute if needed |
| Crypto Officers (COs) | Holders of activation cards, drawn from **different institutions** (see Layer 2) | Activate the hardware module and vouch publicly for the ceremony |
| Safe Security Controllers (SSC1, SSC2) | Two different people | SSC1 opens the equipment safe; SSC2 opens the credentials safe; each logs every item removed and returned |
| System Administrator | County IT | Runs cameras, livestream, and room access; never touches keys |
| External Auditor | The named outside auditor | Attests the ceremony followed the script; reviews the recordings |
| External Witnesses | Public, press, Quorum Court members | Observe |
| Ceremony clerk (LLM) | Offline local model (`ceremony-clerk.md`) | Advisory only. Its transcript is secondary and is compared against the IW's record afterward |

## Layer 2: M-of-N activation across institutions

- The hardware module needs **3 of 5** activation cards (ICANN uses 3 of 7).
- Cards go to five **separate institutions**, so no single office can act alone:
  1. Clark County Sheriff's Office
  2. County Clerk
  3. The outside auditor
  4. A citizen oversight board member
  5. A faculty member from Henderson State University or Ouachita Baptist University (both in Arkadelphia)
- No institution holds more than one card. The builder (Brayden) holds none.
- At least 4 COs are invited to each ceremony, so one absence doesn't stall it.

## Layer 3: Physical custody

- **Two safes in one locked room.** Safe 1 holds equipment: the hardware module(s), the offline laptop, the verified OS disc, and blank write-once media. Safe 2 holds credentials: the activation cards.
- In Safe 2, **each card sits in its own lockbox requiring two physical keys**, one held by the county and one by that card's CO. ICANN uses this same dual-key box.
- **Tamper-evident bags (TEBs)** with serial numbers on every hardware module, laptop, and card. Serial numbers are recorded when sealed and **checked against the previous ceremony's record** when opened. Any mismatch stops the ceremony.
- **Dual occupancy:** nobody is ever alone in the room or at an open safe.
- Hardware modules are chosen to **wipe themselves on tamper detection**.

## Layer 4: Clean equipment, every time

- The offline laptop has **no internal storage, no wireless, and no network hardware.** Remove it physically rather than disabling it in software.
- It boots from a **read-only OS disc** whose hash is published and checked at the start of each ceremony.
- Every artifact brought in (software builds, the LLM model file) is on write-once media, and its hash is checked against the **pre-published reproducible-build hash** before use.
- After the ceremony, the laptop is powered off and resealed. Nothing persists on it.

## Layer 5: Scripted procedure

- The **script is published in advance**, with a public comment window before the first ceremony.
- **A dry run** precedes the first live ceremony.
- The CA **reads each step aloud.** The IW confirms and timestamps it.
- **Any deviation is an exception:** stop, record it, and have the auditor rule before continuing. Nobody improvises.
- Core sequence:
  1. Verify room and attendee list.
  2. Check TEB serials against the last record.
  3. SSC2 opens Safe 2 and COs retrieve cards from their dual-key boxes.
  4. SSC1 opens Safe 1 and equipment comes out of its TEBs.
  5. Boot from the verified disc.
  6. Verify artifact hashes.
  7. Three COs activate the module.
  8. Perform the ceremony actions (generate, pin, sign), receipts only.
  9. Deactivate.
  10. Reseal everything in **new** TEBs and record the new serials.
  11. Return items to the safes.
  12. All participants sign the IW's script.

## Layer 6: Recording and publication

- Film continuously from multiple angles. Nothing secret is ever visible, by design (tools return receipts only), so **everything can be filmed.**
- **Livestream it publicly**, as ICANN has done since 2018.
- Publish afterward:
  - the signed script and exception reports
  - TEB serial records
  - artifact hashes and public-key fingerprints
  - the auditor's attestation
  - the video

  Mirror all of it to a public append-only location.
- Print the audit logs, and give multiple copies to the auditor and the clerk.

## Layer 7: Abort, recovery, and term limits

- **Abort rule:** any TEB mismatch, hash mismatch, missing quorum, or unexplained event stops the ceremony. Reschedule; never push through.
- **Lost or compromised card or module:** follow a pre-written revocation plan. Revoke the affected keys publicly, then hold a new ceremony. Whether a given key type may be backed up at all follows the independent reviewer's guidance; some signature types must never have copies.
- **CO terms are fixed** (for example, 2 years, staggered). Replacing a CO is itself a recorded ceremony step.
- Background checks for COs, SSCs, and the CA as required by ACIC/CJIS where they apply.

## Layer 8: The clerk inside the protocol

- The LLM clerk (`ceremony-clerk.md`) advises the CA. It does **not** replace the IW.
- After each ceremony, the clerk's transcript is compared line by line with the IW's signed record. Any discrepancy is logged and reviewed. That comparison is itself a recurring eval of the model.

---

## Cost reality

- **People:** about 8–12 per ceremony, for a few hours, 1–3 times a year.
- **Equipment:**
  - two safes
  - dual-key lockboxes
  - TEBs (cheap, serialized)
  - hardware modules or tokens
  - one storage-less laptop
  - cameras
- **The real cost is coordination across five institutions.** That cost is the security: it's what makes collusion hard.

## Build tasks for local Claude Code

1. Turn Layer 5 into a full ceremony script template (numbered, read-aloud wording, IW checkboxes, exception form).
2. TEB serial registry: a simple tool that records seal and open serials and flags mismatches against the prior ceremony.
3. Pre-ceremony publication package generator (script, artifact hashes, OS disc hash).
4. Post-ceremony publication package generator (signed script scan, exceptions, serials, fingerprints, attestation slot).
5. Clerk-vs-IW transcript diff tool.
