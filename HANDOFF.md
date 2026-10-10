# Handoff — status as of Oct 10, 2026

## Where things stand

- Research is done (see `research/`). The thesis and legal framing are settled (see `CLAUDE.md`).
- Legal Reference PDF emailed to Sheriff Jason on Oct 9.
- Meeting with the sheriff and Chief Jackson is set. The date is not recorded.
- Nothing is built yet. No hardware has been bought.

## The gate

Nothing public gets built until two things happen:
1. **ACIC confirms how LPR systems receive hotlist data**, and whether a county server holding a hotlist becomes a CJIS system. Brayden should make this call jointly with the sheriff's ACIC person, once the sheriff agrees. ACIC: (501) 682-2222. See `research/05-acic-call-prep.md`.
2. **The Quorum Court passes the ordinance.**

The private-property lot rig (task 1 below) is not gated. It's legal now under § 12-12-1803 with a 60-day retention cap.

## Prioritized next tasks for local Claude Code

1. **Ozark lot proof-of-concept (do first; it's the demo).** Stand up Frigate with LPR at the Arkadelphia Ozark Cleaners lot.
   - Produce a parts list: one dedicated LPR camera with native RTSP and IR, plus a mini PC (AVX2, at least 8 GB RAM) and optionally a Coral or Hailo accelerator.
   - Write a `docker-compose.yml` and a Frigate config with `lpr` enabled and a dedicated LPR camera type.
   - Enforce a **60-day retention** cap. That's the private-owner limit, and the design should prove auto-delete from day one.
   - Goal: "come see it running" is true before the meeting.
2. **Prototype the logged front door** (`design/architecture.md`). This is the part that differentiates the project. Build it in this order:
   1. A small service in front of the plate-read store. Every query requires an individual login and a case number.
   2. An append-only hash-chained audit log of those queries.
   3. A script that publishes the current root hash so an outside witness can pin it.
   4. A verifier that detects any rewrite.

   Plate detection is commodity. This layer is the product.
3. **Retention enforcer.** A scheduled job that hard-deletes reads past the cap and writes its own log entry for each run, so deletion is provable.
4. **Public report generator.** Produce the § 12-12-1805 semiannual stats (scans, lists checked, matches, arrests, prosecutions), plus query volume and sharing recipients.
5. **Ordinance draft support.** Help Brayden turn the 8 commitments in `docs/legal-reference.md` into a starting draft for county counsel. Base it on the CCOPS model plus Somerville's exclusion clause. Mark it clearly as a draft for an attorney.

## Open questions (Brayden to answer)

- When is the meeting?
- When does Arkadelphia's Flock grant end, and what does renewal cost?
- Is this a paid contract, a donation, or a hybrid? Decide before the sheriff asks.
- Who is the outside auditor: a citizen board, the county clerk, or someone else?
- Will any federal money be involved? (NDAA §889 affects which cameras are allowed.)

## Artifacts that also exist online (claude.ai)

These are the same content as `docs/`, viewable or editable in Brayden's claude.ai artifacts:
- ALPR Meeting Brief
- ALPR Blueprint
- ALPR Legal Reference (doc)
- ALPR Action Plan (doc)
