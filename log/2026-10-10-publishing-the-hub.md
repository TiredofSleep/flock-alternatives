# Session log: publishing the hub (Oct 10, 2026)

A conversation between Brayden Sanders and Claude Code, posted as-is apart from formatting. It records
how this repo was published, what was added, and what is still unfinished.

---

**Brayden:** publish as is... just make sure that we are promoting the options available... this is a
flock alternative research hub

**Claude Code:** Your handoff is now public as-is, as a Flock alternatives research hub:
https://github.com/TiredofSleep/flock-alternatives

The new front page lays out every option side by side, not just ours:

| option | in short |
|---|---|
| Stay with Flock and add oversight | the cheapest change; the data stays in Flock's cloud |
| Switch to a vendor with local storage | Rekor, Leonardo/ELSAG, or Axon, which is what Bernalillo County NM did |
| County-owned, open source | your plan, linked to the civic-lightlog prototype |
| Hybrid | a vendor's cameras feeding county-owned storage and logs |
| No plate cameras at all | as Ypsilanti MI chose |

- **The main message:** whichever option a town picks, the protection comes from the rules. That means
  a CCOPS-style ordinance, evidence from improper searches thrown out, an outside auditor reviewing the
  logs often, and public reports that name who the data was shared with.
- **Cost:** the page compares Flock and self-hosted costs, labelled as estimates to check locally.
- **Map:** it lists every document and what it covers.
- **Status:** it's marked as research in progress and not legal advice. Documents are under CC BY 4.0,
  so other counties can adapt them with credit.

Also done:
- civic-lightlog and the hub now link to each other.
- The rate-limit and key-share work in civic-lightlog is committed and pushed. The attack results are
  unchanged: 12 held, 2 still open.

Still missing from the hub: `ceremony-protocol.md`, `sentinels.md` and `ceremony-clerk.md`. They aren't
on this computer, so they're probably still in your claude.ai chat. Download them and I'll add them to
`design/`.

Since CLAUDE.md, the meeting brief and the action plan are now public, assume Chief Jackson and Sheriff
Jason may have read them before you meet. The notes are respectful. Just walk in expecting that they've
seen your strategy.

---

**Brayden:** the files are in downloads

**Claude Code:** I found the files in your new download and added all three to the hub's `design/`
folder. They're described on the front page and pushed (commit 4a8ae93).

- **`sentinels.md`:** a small agent on every machine that only sends. Every hour it sends an outside
  witness a signed summary of that machine's log, then destroys the key it signed with. A stolen key
  can't rewrite earlier history, and a machine that goes quiet raises the alarm. It also covers decoy
  plate records that only a fishing search would hit.
- **`ceremony-protocol.md`:** the eight-layer key ceremony modeled on ICANN's.
- **`ceremony-clerk.md`:** the optional offline AI helper for the ceremony. It only gets receipts back,
  never secrets, behind a fixed rule-checker and a physical button press.

The newer zip and its copy of HANDOFF-UPDATE-2.md matched what I'd already published. The `(1)` copy of
HANDOFF-UPDATE-2 is an older draft without the ceremony section, so I left it out.

Your `sentinels.md` overlaps with civic-lightlog, and the two take different routes:
- **Signatures:** your spec uses standard Ed25519 keys; the prototype uses quantum-resistant hash-based
  signatures. Either works, and the independent security review should make the final call.
- **Decoy records:** they're the same idea as the "mystery shopper" test plates in civic-lightlog. Your
  spec adds the safety rule that matters: never use a plate number that could belong to a real person.
  That waits on the Arkansas DFA confirming a format that can never be issued.

---

**Brayden:** build the ceremony tooling from task 10

**Claude Code:** A safety classifier stopped my response partway through the ceremony tooling build, and
I can't continue that build in this conversation. Of the five pieces of task 10, only the script
template's data file got written: `tools/ceremony/script.json`, the 13 read-aloud steps with the witness
checks and stop conditions. The program that uses it (the printable script, bag-serial registry, before
and after publication packages, and transcript comparison) was never created. Nothing was committed or
pushed.

Options:
- Take task 10 to a fresh session, using `design/ceremony-protocol.md` and `script.json` as the
  starting point.
- Do the steps by hand for now. The 13 steps already work as a paper checklist: the administrator reads
  each one, the witness ticks and signs it, and the bag serials go in a ledger.
- Remove `script.json` so the local folder matches what's published.

---

**Brayden:** at least publish the research and where it points

**Claude Code:** A safety classifier stopped me while I was writing a shareable page, so I couldn't
build that page in this conversation. The half-written file was deleted and nothing from it was
published.

The research is already public in this repo:
- **The front page** lays out every option side by side, with the Flock vs. self-hosted cost
  comparison.
- **What the research says**, in `research/` and `docs/legal-reference.md`: Arkansas law (A.C.A.
  §§ 12-12-1801–1808, Act 668 of 2025), the CJIS/ACIC boundary, governance precedents such as CCOPS,
  Oakland and Somerville, case law, vendors, costs and the maintenance risk.
- **Where it points**, in `docs/action-plan.md`, `HANDOFF.md` and `design/`: call ACIC first, pass the
  ordinance before any cameras go up, run a small county-owned pilot with one logged front door and an
  outside auditor, then commission an independent security review before going live.
- **The working prototype** is at https://github.com/TiredofSleep/civic-lightlog.

---

## Status at the end of this session
- **Published:** the research, legal reference, action plan, meeting brief, blueprint, architecture,
  sentinel design, ceremony protocol, ceremony clerk spec, handoffs, and the encryption discussion
  transcript (`research/06-encryption-discussion.md`).
- **Not built:** the task 10 ceremony tooling. A draft step list (`tools/ceremony/script.json`) exists
  locally only.
