# Build path, CJIS, and cost reality

Research digest, Oct 9, 2026. Cost figures marked "estimate" are build-up estimates, not single-source citations.

## Software stack
- **OpenALPR is dead.** Its last release was 2.5.103 (Mar 2018); Rekor acquired it in 2019 and ended the free tier. ([Wikipedia](https://en.wikipedia.org/wiki/OpenALPR))
- **Frigate NVR LPR:** YOLOv9 plate detector plus PaddleOCR, small or large models. Needs at least 4 GB RAM and an AVX/AVX2 CPU. Per its own docs: "if a human can't read the characters, Frigate usually can't either." Fast vehicles need a higher detect FPS. No published accuracy numbers. ([docs](https://docs.frigate.video/configuration/license_plate_recognition))
- **fast-alpr:** MIT license, ONNX, swappable backends. ([GitHub](https://github.com/ankandrew/fast-alpr))
- **Platerecognizer:** paid, fully on-prem in Docker, claims about 95% accuracy. ([site](https://platerecognizer.com/better-than-openalpr/))
- **Verdict:** good for driveways and slow approaches, marginal at highway speed. Tune each site.

## Cameras
- Shutter speed matters more than megapixels: at least 1/1000s, and 1/2000s at night or speed. Aim for about 100 pixels per foot on the plate. Use IR, and expect focus to shift between IR and visible light. ([ipcamtalk](https://ipcamtalk.com/goto/post?id=313506))
- Fixed lenses at 55+ mph are where DIY setups break down. Buy motorized varifocal.
- Dahua/EmpireTech LPR line, e.g. DH-ITC215-PW6M-IRLZF (2MP, 3.2–10.5mm motorized, 12m IR, ~$300–450). ([UHS](https://www.uhs-hardware.com/products/dahua-ip-2mp-lpr-bullet-camera-motorized-varifocal-3-2-10-5mm-lens-outdoor-wdr-ip67-12m-ir-license-plate-recognition-5-year-warranty-dh-itc215-pw6m-irlzf-b))
- **NDAA §889:** Hikvision and Dahua are barred for federal or federally funded purchases. Verify before buying.
- Solar plus LTE pole site: about $800–2,500 (estimate).

## CJIS and ACIC
- Small Arkansas agencies usually have **ACIC Indirect Access**: they can receive CJI but can't run transactions directly. Recipients must have an FBI-assigned ORI. ([agreement](https://dps.arkansas.gov/wp-content/uploads/2020/05/Indirect_Access_Agency_Agreement_2018.pdf))
- Capturing plates is **not** CJIS-regulated. Crossing them against NCIC/ACIC hotlists **is**.
- If the system touches CJI, CJIS requires:
  - MFA
  - FIPS-validated encryption in transit and at rest
  - Audit logging with actual weekly review
  - Least privilege, plus lockout after 5 failed attempts
  - A fingerprint check within 30 days for anyone with access, including IT staff and vendors; a felony bars access
  - CJIS security training
  - An FBI Security Addendum in vendor contracts, sent to ACIC

  ([overview](https://www.saltycloud.com/blog/cjis-requirements/))
- ACIC audits agencies with direct access at least every 3 years and runs CJIS IT audits across 13 policy areas. Agencies must file action plans within 30 days of findings. ([Audit Policy May 2026](https://dps.arkansas.gov/wp-content/uploads/Audit-Policy-5-4-2026.pdf))

## Vendors
From the ACLU's Aug 2026 survey ([ACLU](https://www.aclu.org/news/privacy-technology/tracking-alpr-cameras/other-alpr-vendors)):
- **Rekor:** allows local install and processing.
- **Leonardo/ELSAG:** runs on local hardware.
- **Axon:** offers a local storage option and case-by-case sharing.
- **Motorola/Vigilant:** no local storage, national network, has an ICE contract.
- **Flock:** cloud only.

No vendor sells full ownership to a 20k-person county. The choice is to self-build or buy a vendor that allows local storage.

## Cost
| | Flock | Self-hosted |
|---|---|---|
| Per camera | $2,500–3,000/yr plus $250–350 install | $300–500 one-time |
| 6–10 cameras | ~$20–30k/yr | ~$15–40k one-time plus server (estimate) |
| Annual | included | LTE $20–50/cam/mo, storage, replacements, **staff time** |

([Flock pricing](https://getsafeandsound.com/blog/flock-safety-pricing/))

## The real risk: maintenance
- GSA: as few as 13% of large government IT projects succeed. GAO: about 80% of federal IT spend goes to legacy maintenance. ([Route Fifty](https://www.route-fifty.com/digital-government/2024/09/governments-often-struggle-massive-new-it-projects/399266/))
- Bus factor of one: the system rots when its one owner leaves or their fingerprint clearance lapses. Budget a permanent fractional FTE.
