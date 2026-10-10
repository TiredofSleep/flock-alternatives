# ACIC call prep

**ACIC:** (501) 682-2222, 322 S. Main St., Ste. 615, Little Rock, AR 72201. Ask for the CJIS Systems Officer or whoever handles interface agreements and LPR hotlist access. The Audit Coordinator knows what a CJIS IT audit expects.

## Who makes the call
- ACIC works only with criminal justice agencies, which need an FBI ORI. To ACIC, Brayden is a prospective vendor.
- **Best:** a joint call with the sheriff's ACIC person, likely his Terminal Agency Coordinator (TAC). Get the sheriff's okay first. Don't recruit his staff before he's bought in.
- Before the sheriff says yes, Brayden can call alone for general information only ("I'm scoping this and want to understand requirements"). He shouldn't claim to be working with the SO.

## Opening
"I'm a local software developer in Clark County scoping a county-owned license plate reader system with the Sheriff's Office. We want to build it the way ACIC requires from day one. Who should we talk to about how LPR systems get hotlist data?"

## Questions, in priority order
1. How do LPR systems in Arkansas receive NCIC/ACIC hotlist data today: an extract file, a live query, or through the agency terminal? (Flock gets it somehow.)
2. What agreement is required (interface, hotlist-use, other), and who holds it: the agency, the vendor, or both?
3. **Does a county-owned server holding the hotlist extract become a CJIS system?** (This is the pivotal question.)
4. Can a county-owned, self-hosted system qualify the same way a vendor cloud does? Has anyone in Arkansas done it?
5. What does ACIC need to see before approving? Get a checklist and document names.
6. Does the hotlist extract have its own retention or refresh rules beyond the Act 668 150-day cap?
7. Would this fall under the sheriff's existing 3-year ACIC audit, or a separate review?

## Expect to hear about Brayden as a vendor
A fingerprint check within 30 days, no felony record, a signed FBI CJIS Security Addendum, CJIS security training, and the county contract sent to ACIC. Answer: "That's expected, I'll do it."

## Reading the answer
- **Green:** hotlist is available to agency-approved systems and matching can run on the agency side. The build is capture plus a local log, with minimal CJIS exposure.
- **Yellow:** "the server becomes a CJIS system." Host on a sheriff-controlled network and budget for a CJIS IT audit.
- **Red:** "approved vendors only." Ask how a vendor gets approved; that becomes the next step.

Write down every name, title, and document mentioned.
