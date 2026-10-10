# System design — county-owned ALPR with one logged front door

Status: a design spec drawn from the research. Nothing here is built yet. The ACIC boundary in section 2 is unconfirmed.

## 1. Components

```
[LPR cameras] --RTSP--> [Edge/NVR: Frigate LPR] --plate reads--> [Read store (Postgres)]
                                                                       |
                                                    every query goes through
                                                                       v
[Users: deputies, investigators] --MFA login--> [Front Door API] --> [Audit log (hash-chained, append-only)]
                                                                       |
                                              root hash published --> [External witness: county clerk / public repo]
[Retention job] --deletes past cap, logs itself--> read store + audit log
[Report job] --> semiannual public report (§12-12-1805 stats + query volume + sharing recipients)
[Hotlist matching] --> ON THE ACIC SIDE if possible (see section 2)
```

## 2. The CJIS boundary (decide after the ACIC call)

- **Preferred:** the county system stores plate reads and a local hotlist only. NCIC/ACIC matching happens through the sheriff's existing ACIC-connected workflow (Indirect Access, via dispatch or a parent agency terminal). The county box is then not a CJIS system.
- **If ACIC says a server holding the hotlist extract is a CJIS system:** host it on a sheriff-controlled network and plan for a CJIS IT audit across the 13 policy areas. Those include MFA, FIPS-validated encryption in transit and at rest, audit review, 5-failed-attempt lockout, and a fingerprint check for every admin and vendor.

## 3. The five pillars and the control that closes each failure mode

| Pillar | Implementation | Documented failure | Required control |
|---|---|---|---|
| Tamper-evident log | Hash chain or Merkle tree. Each entry hashes its content plus the previous hash. Consider Google Trillian, or a simple chain over Postgres with WORM/object-lock backup. | No one outside checks it, so an admin with the key and the DB can rewrite and re-sign. "Tamper-evident to nobody." | **External witness.** Publish the signed root hash on a schedule to a place the county doesn't control (clerk, public git repo). The verifier compares against pinned roots. |
| One front door | All reads come through one API. There is no direct DB access for users and no national-lookup feature. | A DEA agent searched under a local officer's password, so the log recorded the wrong person. | Individual accounts only, hardware MFA, zero shared or service accounts for humans. |
| Reason per query | Each query requires a case number. | Flock's free-text reasons ("idk", "LMAO", "TBD"; one "idk" search hit 82,413 cameras). A dropdown "fix" just became a rubber stamp. | **Validate the case number against a real case record** (RMS or case list). No valid open case means no search. |
| Unauthorized = crime | The ordinance makes access outside the front door misconduct, with an exclusion clause. | California agencies had a logging law and did "little to no auditing." CJIS audits only every 3 years. | A named outside auditor with a short review cadence (weekly or monthly), plus automated anomaly flags: bulk searches, off-hours use, one user with many plates. |
| Public reporting | A report generator. | Flock portals publish only flattering aggregates; abuses surfaced through FOIA. | Publish sharing recipients, query counts per user role, anomaly counts, and audit findings. |

## 4. Audit log entry (minimum fields)

`seq, timestamp_utc, user_id (individual), auth_method, case_number, case_validated (bool), query_type, query_params (plate/partial/description), result_count, requesting_agency, shared_with (if any), legal_basis (warrant/court order/hotlist/none), prev_hash, entry_hash`

Retention and deletion runs also write entries: `job_id, rows_deleted, oldest_remaining_ts`.

## 5. Retention

- Government cap is 150 days, unless the data is tied to an open investigation; it's deleted when the case closes. Private lot (pilot) cap is 60 days.
- Enforce in software with a scheduled hard delete. Log each run. Report "nothing older than cap" as a pilot success metric.

## 6. Sharing (if federated later)

- Opt-in per recipient. Each share is a logged query, not a data copy ("is this plate on your list?", logged on both ends).
- Links are revocable and expire unless renewed.
- One named body audits anything that crosses a jurisdiction line. That is the fusion-center and LInX lesson.

## 7. Stack notes

- **Detection and OCR:** Frigate NVR's built-in LPR (YOLOv9 detector, PaddleOCR; at least 4 GB RAM, AVX/AVX2 CPU). Alternative: fast-alpr (MIT, ONNX). Paid self-hosted fallback: Platerecognizer.
- **Cameras:** dedicated LPR/ANPR with native RTSP/ONVIF, at least 1/1000s shutter, IR, motorized varifocal. Dahua/EmpireTech ITC215-PW6M-IRLZF runs about $300–450, but check NDAA §889 if federal money is involved. Amcrest and Reolink are fine for slow approaches like a parking lot.
- **Off-grid poles:** LPR camera plus edge compute plus LTE modem plus solar and battery, roughly $800–2,500 per site.
- **Open-source all of it** so the county is never locked to any one maintainer.
