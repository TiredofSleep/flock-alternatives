# Handoff update 2 (Oct 10, 2026, late morning)

Drop this file and `design/sentinels.md` into your local `alpr-handoff/` folder. Everything else from the first handoff is unchanged.

## New since the first handoff

### 1. `design/sentinels.md` (new file)
A spec for "one-way sentinels" on every machine:
- **Sentinel agents:** a small agent on each machine pushes signed checkpoints of its audit log to an outside witness. It is outbound-only and rotates its signing key each epoch, committing to the next key in every checkpoint, so earlier history can't be re-signed.
- **Silence is the alarm:** the witness alerts on missed checkpoints, broken chains, or bad signatures.
- **Canary records:** fake plate reads that only dragnet or fishing queries would hit. Hard rules: never a real plate, excluded from stats, reports, and evidence exports, and seeded by the outside auditor.
- **Who controls what:** county IT never controls the witness, the starting-key pinning, or the canaries.
- **Build order:** checkpoints plus the silence alarm in the pilot; a verifier CLI; canaries later; a hardware data diode only if the system scales.

### 2. Principles agreed in discussion (add to CLAUDE.md under the thesis)
- **No barrier is uncrossable, so the design relies on deletion and witnessing.** Retention deletion is the strongest security feature: data that no longer exists can't be subpoenaed, leaked, or decrypted later. Witnessing makes every crossing leave a trace.
- **Encryption strength isn't the weak point.** Every documented ALPR abuse was a person with valid credentials, a setting, or a legal demand. Design effort goes to identity, review, and deletion, not exotic cryptography.
- **Kerckhoffs's principle:** security lives in the keys, never in secret or complicated machinery. All code and the design stay public. Add independent layers that fail differently; don't add more gears to one layer.
- **Born offline:** release-signing keys and each sentinel's starting key are created on an air-gapped machine in a witnessed, scripted ceremony with the outside auditor present. Builds should be reproducible, so anyone can confirm a binary matches the public source.

### 3. New required gate before any public deployment
- **An independent security review** of the full system (software, sentinel, and any hardware) by an outside firm before go-live. Findings go into the public pilot report to the Quorum Court. Add it to the pilot budget.
- Reviewers should start from:
  - [NIST stateful hash-based signatures / SP 800-208](https://csrc.nist.gov/Projects/stateful-hash-based-signatures)
  - [EmLog: tamper-resistant logging on constrained devices](https://arxiv.org/pdf/1712.03943)

### 4. New open questions
- **Arkansas DFA:** is there a plate-string format that can never be issued, which would make canary records safe? This gates canaries.
- **Who runs the witness?** The county clerk, a university, or a third party, plus a public mirror so the witness can't drop entries quietly.
- **Who pays for, and selects, the independent security review?**

## Tasks for local Claude Code (in addition to tasks 1–5 in HANDOFF.md)
6. **Silence alarm + checkpoint receiver (witness side).** An append-only endpoint that accepts signed checkpoints, verifies the chain against a pinned starting key, and alerts after 2 missed epochs. Use it with the task 2 audit log.
7. **Verifier CLI.** Anyone can walk a machine's published checkpoint chain and confirm it's intact.
8. **Ceremony runbook (draft).** A step-by-step, two-person, witnessed procedure for generating and pinning keys on an offline machine, written for the outside auditor to follow and sign. Mark it as a draft pending independent review.

## Added: ceremony clerk (`design/ceremony-clerk.md`)
A purpose-built local LLM that assists the offline key ceremony. **It gets tools but no visibility:** every tool returns only receipts (handle IDs, public fingerprints, ok/fail) and never secret material. Every tool request passes a deterministic gate plus a physical two-officer authorization on the hardware token.

9. **Build the ceremony clerk in the spec's order:** checklist engine, then gate, then receipt-only tool stubs, then eval harness, then the model last. Register the kill conditions before the first test. The gate is PROVED; the model is MEASURED.

## Added: ceremony protocol (`design/ceremony-protocol.md`)
An 8-layer key ceremony modeled on ICANN's root KSK ceremony and scaled to the county:
1. Separated roles, with no person holding two.
2. 3-of-5 activation cards held by five separate institutions; the builder holds none.
3. Two safes, with dual-key lockboxes and serialized tamper-evident bags checked against the last ceremony.
4. A storage-less offline laptop booted from a hash-verified read-only disc.
5. A published, read-aloud script with exception handling.
6. Filmed, livestreamed, and fully published.
7. Abort rules, a revocation plan, and term limits for card holders.
8. The LLM clerk as advisory only, with its transcript diffed against the human witness's record.

10. **Build the ceremony tooling:** script template, tamper-bag serial registry, pre- and post-ceremony publication packages, and the clerk-vs-witness transcript diff tool.
