# Design addendum: one-way sentinels

Addendum to `architecture.md`. Status: a design spec, nothing built. Origin: Brayden's idea of "one-way sentinels in every machine, changed periodically."

## The problem this closes

`architecture.md` makes the audit log tamper-evident *if* someone outside checks it. Two holes remain:
1. **An admin who holds the signing key** can rewrite history and re-sign it.
2. **A dragnet or fishing query** that is properly logged still only gets noticed if someone reads the log carefully.

The sentinels close both: (A) rotating one-way signing agents, and (B) rotating canary records.

---

## A. Sentinel agents (forward-secure, outbound-only)

### What it is
A small agent runs on every machine: edge box, NVR, read store, front-door API. It periodically pushes a **signed checkpoint** of that machine's audit log to the external witness. It sends only. It accepts no inbound commands.

### Forward security (the "changed periodically" part)
Use per-epoch Ed25519 keypairs in a chain:

```
epoch i checkpoint = {
  machine_id, epoch=i, timestamp,
  log_head_hash,          # hash of the last audit-log entry in this epoch
  entry_count,
  next_pubkey = PK_{i+1}  # commit to the next epoch's key
}
signature = Sign(SK_i, checkpoint)
→ send to witness, then DESTROY SK_i (overwrite in memory, never written to disk)
```

- The witness pins `PK_0` for each machine at install time. This must be done **in person, by the outside auditor**.
- The verifier walks the chain: each checkpoint must verify under the pubkey committed in the previous checkpoint.
- **Property:** an attacker who steals the current key `SK_n` cannot forge checkpoints for any earlier epoch, because those private keys no longer exist. History before the compromise is permanently locked.
- Epoch length starts at 1 hour. Shorter epochs mean less history exposed per stolen key.
- References: Schneier & Kelsey, "Secure Audit Logs to Support Computer Forensics" (1998); Bellare & Yee, forward-secure MACs/signatures.

### Outbound-only
- **Pilot:** the witness exposes a single append-only HTTPS endpoint, reachable only by sentinel keys. The sentinel has no listener and no remote-config path.
- **Later, optional:** a hardware **data diode** (physically one-direction link) between the county network and the witness. Utilities and the military use these. Overkill for the pilot.

### Silence is the alarm (dead-man's switch)
- If a machine misses its checkpoint by 2 epochs, the witness alerts the outside auditor.
- If the epoch count skips, the chain breaks, or a signature is invalid, the witness alerts immediately.
- **Why:** an attacker on the machine can kill the agent. They can't make the witness *not notice* that it went quiet.

### Who controls what
| Thing | Controlled by | Never by |
|---|---|---|
| `PK_0` pinning at install | Outside auditor, in person | County IT |
| Witness server and alerting | Outside auditor / third party (clerk, university, or a public repo plus a monitor) | County IT or the sheriff's office |
| Sentinel code | Open source, published hash of each release | Anyone silently |

---

## B. Canary records (honeytokens)

### What it is
Seed fake plate reads into the read store that **no legitimate query should ever touch**. Any query that returns one is logged as a canary hit and alerts the auditor.

- A legitimate search, meaning a specific plate tied to a validated case number, never hits a canary.
- A dragnet, fishing query, bulk export, or exfiltration dump does.
- Rotate the set on a schedule (for example monthly) so insiders can't learn which records are fake.

### Hard rules
1. **Never a real plate.** A fake read on a real plate puts a real person somewhere they weren't, inside an evidentiary database. Use plate strings that are **not issuable** under Arkansas formats, or vehicles the county itself controls and registers for this purpose. Confirm the non-issuable format rules with the Arkansas DFA before seeding.
2. **Invisible to users, but known to the system.** Flag canaries in a separate table or keyed list that only the auditor-controlled process can read. The front-door API strips them from results it returns and logs the hit.
3. **Excluded from everything official:** the Act 668 §1805 semiannual stats, public reports, evidence exports, and anything that reaches a courtroom. Write a test proving a canary can never appear in an evidence export.
4. **Seeded by the outside auditor**, not county IT. Whoever plants the canaries knows the map.

### Canary hit record
`seq, timestamp, user_id, case_number, query_params, canary_id, result_count, query_shape (exact / partial / description / bulk)` is written to the main audit log and pushed immediately to the witness, without waiting for the epoch checkpoint.

---

## Build order (keep it simple; this is a ~10k-person county)

1. **Forward-secure checkpoints plus the missed-heartbeat alarm.** This is the highest value and the least complexity. Build it into the pilot.
2. **Verifier CLI.** Anyone, including a journalist or defense attorney, can walk a machine's checkpoint chain against the published `PK_0` and confirm integrity.
3. **Canary records.** Add only after the pilot proves the basics, and only after the DFA confirms a non-issuable plate format.
4. **Hardware data diode.** Only if the system scales past the pilot.

## How each piece fails

- **Key generation on a compromised machine at install** means a forged `PK_0`. Fix: generate on a fresh, offline device during the in-person install, with the auditor present.
- **The witness itself is the single point of trust.** Fix: mirror checkpoints to a public append-only location too, such as a public git repo, so the witness can't quietly drop entries.
- **Alert fatigue.** Missed heartbeats from flaky LTE poles will cry wolf. Fix: alert thresholds per site type, with every alert logged so there's a record if the auditor starts ignoring them.
- **Maintenance burden.** Every layer is something to patch. Fix: open-source everything, document it, and skip step 4 unless there's a real reason to do it.
