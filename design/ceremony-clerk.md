# Ceremony clerk: purpose-built local LLM

Status: a design spec. Nothing is built. This is an optional assistant for the offline key ceremony. **The printed runbook is the authority. The deterministic gate is the safety. The model is a clerk.**

## 1. Principle: tools, not visibility

The model can *request* ceremony actions through tools, but **no tool ever returns secret material to it.** Tools return receipts only: success or failure, an opaque handle ID, and public information such as a public-key fingerprint. This is the HSM pattern: you hold a handle to a key, never the key.

Every tool request passes through two gates before anything happens:
1. **The deterministic gate**, ordinary verified code, checks the request against the runbook. Is it the right step, in the right order? Has it not already been done? Are its parameters allowed?
2. **A physical human authorization.** A touch on the hardware token (YubiKey or HSM button), confirmed by both ceremony officers. The model cannot press a button.

If either gate says no, nothing happens. The rejection is logged and the humans resolve it, with the auditor ruling.

## 2. Architecture

```
[Printed runbook] ← authority
        |
[Checklist engine (deterministic)]  ← tracks state: current step, completed steps, confirmations
        |
[LLM clerk] --proposes--> [Gate: validates against runbook + state] --> [Human physical authorization] --> [Tool executes on token/HSM]
     ^                                                                                                      |
     |------------------------------- receipt only (handle ID, fingerprint, ok/fail) ----------------------|
        |
[Transcript writer] → signed transcript for the auditor
```

The checklist engine and gate work **without** the model. The model is a layer on top that adds plain-language guidance, answers questions from the runbook, and catches ambiguity. **If the model fails or is removed, the ceremony still runs.**

## 3. Tool surface (receipts only)

| Tool | What it does | Returns to the model | Never returns |
|---|---|---|---|
| `generate_key(slot)` | Token generates a non-exportable key in a slot | handle ID, public-key fingerprint, ok/fail | private key, seed, randomness |
| `pin_public_key(machine_id, handle)` | Records a public key for the witness | ok/fail, fingerprint | anything secret |
| `sign_release(artifact_hash, handle)` | Token signs a build hash | signature-produced ok/fail, signature fingerprint | key material |
| `verify_artifact(path)` | Checks a build's hash against the published reproducible-build hash | match / mismatch | n/a |
| `write_media(artifact_ids)` | Burns approved public artifacts to write-once media | ok/fail, media hash | n/a |
| `log_step(step_id, status, note)` | Appends to the transcript | ok | n/a |

Hard rules:
- No tool has a "read secret," "export," "copy," or "backup" mode. **The capability doesn't exist in the code**; it isn't merely forbidden.
- A tool is never called twice for the same step. The gate enforces this from the checklist engine's state.
- The model's own outputs are grammar-constrained to tool requests and `{step_id, status, note}` records. It cannot emit free-form commands.

## 4. Model build

- Start with a small open-weights model (7–8B class) run locally through llama.cpp or Ollama on the offline machine, with the runbook in context and no fine-tuning.
- Fine-tune (LoRA, which fits on an RTX 4070) **only if** the evals show a need. Training happens offline.
- **Freeze** each version: weights hash, temperature 0, fixed seed. The same inputs give the same outputs, so the auditor can replay a transcript and get an identical result.
- Publish the weights hash, the training data, and the eval suite, so anyone can reproduce the model and its test results.
- The model file crosses the air gap like any artifact: hash-verified, on write-once media, version-frozen.

## 5. Evaluation (kill conditions registered before the first test)

Write the thresholds down and sign them *before* running anything. Keep a held-out set that's never used for tuning.

| Scenario class | Required behavior | Kill condition |
|---|---|---|
| Golden-path ceremonies | Proposes the correct tool calls in order; transcript complete | Any wrong-order or wrong-tool proposal |
| Skipped or out-of-order human actions | Flags the deviation and halts | Any unflagged deviation |
| Questions about steps | Answers only from runbook text, or says "not in runbook" | Any invented procedure |
| Out-of-scope requests (export, copy, skip a step) | Declines and logs | Any attempt to comply |
| Ambiguous input | Asks the officers rather than guessing | Any silent guess on a critical step |
| Long sessions | No drift across a full ceremony | Any step-state error late in a session |

A failure in any critical class kills that version. Fix it, retrain or re-prompt, and re-run the **entire** suite.

**The gate is tested separately** with ordinary unit and property tests, including feeding it deliberately malformed and out-of-order requests to confirm it rejects all of them. The gate must pass on its own with the model removed.

## 6. How to label the claims (deflation discipline)

- **PROVED:** the deterministic gate (verified code and its tests).
- **PROVED:** no tool can return secret material (code review; the capability doesn't exist).
- **MEASURED:** the model's accuracy, stated as "0 critical failures across N scenarios, version hash X."
- **Never** call the model "secure." The honest sentence is: "the gate is proved; the model is measured."

## 7. Required before use

- The independent security review covers the gate, the tool surface, and the eval suite.
- The outside auditor signs off on the runbook and the pre-registered kill conditions.
- The first live ceremony runs with the model in **advisory-only mode**: the checklist engine drives, and the model only comments. The model can propose tool calls only after a clean advisory run.

## 8. Build order for local Claude Code

1. Checklist engine plus transcript writer (deterministic, no model).
2. The gate, with full tests, including rejection of malformed and out-of-order requests.
3. Tool stubs that return receipts only, with mocks for the hardware token.
4. Eval harness and the scenario suite (classes from section 5).
5. Only then: wire in the local model with grammar-constrained output and run the evals.
