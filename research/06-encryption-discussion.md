# Transcript: does encryption solve this? (and where the sentinels came from)

A conversation between Brayden Sanders and Claude (claude.ai), Oct 2026, posted as-is apart from
removed interface labels. It is the reasoning behind `design/sentinels.md` and the principles in
`HANDOFF-UPDATE-2.md`. Not legal or security advice; claims should be checked against sources.

---

**Brayden:** Handed off... seems like until we make quantum entangled encryption locally available,
there is no barrier that can't be crossed...

**Claude:** The barrier was never the math, and quantum won't fix the part that actually breaks.

The crypto already holds. AES-256 isn't getting brute-forced by anyone, the NSA included. Even a large
quantum computer only halves its effective strength (Grover's algorithm), which still leaves 128 bits:
heat-death-of-the-universe territory. The part quantum computers would break is today's public-key math
(RSA, elliptic curves, via Shor's algorithm). NIST already standardized the replacements in 2024 (ML-KEM
and ML-DSA, FIPS 203/204). Those are ordinary software that runs on a laptop, available now, no physics
required.

Entanglement-based encryption (QKD) protects the wire, which was never the weak spot. QKD lets two
endpoints detect anyone eavesdropping on the link between them. It has real limits:

* It only works point-to-point over a dedicated fiber or line of sight.
* It still needs classical cryptography to authenticate who's on each end.
* It does nothing once data is sitting on a server.

The NSA actually advises against relying on it. It's a perfect lock on a pipe nobody was breaking into.

How these systems actually fall, every case in your research:

* A DEA agent logged in with a local cop's password.
* Officers typed "idk" as their reason and searched 82,000 cameras.
* California agencies kept logs that nobody read.
* Flock flipped a sharing setting on by "miscommunication."

Not one of these was a cryptographic failure. Every one was a person with legitimate keys, or a
setting, or a subpoena. You can't encrypt your way out of an insider holding valid credentials, and
you can't out-math a court order.

That's why the design you landed on is right. The two strongest defenses in your system aren't
encryption:

1. **Deletion.** Data deleted on day 150 can't be subpoenaed, leaked, stolen, or decrypted in 2040 by a
   quantum computer. Nonexistence is the only barrier that truly can't be crossed. The retention job is
   your strongest security feature.
2. **Witnessing.** You accepted that a determined actor can get in, so you made sure they can't get in
   unseen. The log doesn't stop the crossing. It makes the crossing cost something.

You're right that no barrier is uncrossable. The answer to that was never a better wall. It's holding
less behind the wall, and making sure any crossing leaves a trace someone outside will see.

---

**Brayden:** Yea, we are thinking one way sentinels in every machine changed periodically

**Claude:** That's a strong idea. It maps to two real techniques, and the combination closes the biggest
hole left in the design: an admin who holds the keys.

**Reading 1: sentinel agents that only talk outward.** Each machine runs a small agent that pushes
signed log checkpoints out to the external witness and accepts nothing back. Rotating its keys gives
you forward-secure logging, a known technique (Schneier & Kelsey, 1998; Bellare & Yee). Each period's
signing key is derived from the previous one, and the old key is destroyed. Someone who steals today's
key can't forge or rewrite yesterday's entries, because the key that signed them no longer exists
anywhere. That kills the "admin with the key re-signs history" attack from the research.

The "one-way" part can be literal. A data diode is hardware that physically allows traffic in only one
direction, and utilities and the military use them. That's overkill for a pilot; a write-only append
endpoint on the witness side is enough to start.

**Reading 2: sentinel records, also called canary tokens or honeytokens.** You seed fake plate reads
into the database that no legitimate search should ever touch. Anyone who hits one, whether through a
bulk search, a fishing query, or an exfiltration dump, trips an alarm. Rotating them means insiders
can't learn which ones are fake. This directly attacks the "idk" search across 82,000 cameras: a
dragnet query lights up the canaries, while a legitimate case-number search for a specific plate never
sees them.

Where it breaks, and the fix for each:

* **A sentinel on a compromised machine can just be killed.** So silence has to be the alarm: if the
  witness doesn't get a heartbeat on schedule, it alerts. A missed check-in is evidence too.
* **Canaries must never be real plates.** A fake read on a real plate puts a real person somewhere they
  weren't, inside an evidentiary database. Use plate strings that can't be issued, or vehicles the
  county controls. Also tag them invisibly so they're excluded from the Act 668 stats, from search
  results, and from anything that reaches a courtroom.
* **Whoever sets the rotation can't be whoever it's guarding against.** If the county admin generates
  the canaries and the sentinel keys, the admin knows the map. Key generation and canary seeding should
  sit with the outside auditor or witness, not county IT.
* **Every layer is maintenance.** This is a ~10k-person county where the bus-factor-of-one problem is
  the main threat. Build the simplest version first: forward-secure log signing plus a missed-heartbeat
  alarm. Add canaries once the pilot has proven the basics.

Put together, the design shifts from "we'll notice if someone tampers" to "tampering destroys the
evidence the attacker would need to hide it, and fishing sets off alarms they can't see." That's about
as close to an uncrossable barrier as software gets. The crossing still happens, but it always leaves
a trace.

Want me to write this up as a design addendum you can drop into the handoff folder for local Claude
Code to build from?

---

**Brayden:** Interesting... thank you... build the handoffs for whatever you can pass to Claude Code
since our last pass

*(That handoff became `design/sentinels.md` and `HANDOFF-UPDATE-2.md`.)*
