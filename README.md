<!-- SPDX-License-Identifier: Apache-2.0 -->
<!-- SZL Holdings — Λ-Conjecture Bounty · the working intake + CI arbiter. -->

# Λ-Conjecture Bounty — intake + CI arbiter (ACTIVE)

This repository is the **working submission intake and automated arbiter** for
**Conjecture 1** (PURIQ formula **F23** — the Λ-aggregator uniqueness conjecture).
It is **NOT** an archived redirect stub — it is live, accepts pull-request
submissions, and runs the `verify-proof` CI that is the *sole, no-bypass* judge.

> **Honest posture.** Λ (the geometric-mean trust aggregator) is and remains
> **Conjecture 1 — NOT a theorem.** The formal statement in
> [`Lambda/Lambda.lean`](Lambda/Lambda.lean) is a `theorem … := by sorry`. Until a
> real proof discharges that `sorry`, the `verify-proof` workflow on `main`
> **intentionally fails** — that red CI state is the public, honest signal the
> conjecture is still open. Do not "fix" CI by removing the `sorry`; only a real,
> axiom-allowlisted proof may turn it green.

- **Doctrine:** v11 — 749 declarations · 14 unique axioms · 163 sorries · `locked_at c7c0ba17`
- **Bounty declaration (founder-set amount):** [`lutar-lean/BOUNTY.md`](https://github.com/szl-holdings/lutar-lean/blob/main/BOUNTY.md)
- **Academic "live home" framing:** [`szl-papers/bounty/`](https://github.com/szl-holdings/szl-papers/tree/main/bounty)
- **Open obligation:** `Lutar/Uniqueness.lean:120` (`CAUCHY_ND` residual) + a missing axiom — see the soundness note below.

## What's in here

| Path | Purpose |
|---|---|
| [`Lambda/Lambda.lean`](Lambda/Lambda.lean) | The formal **Conjecture 1** statement (`theorem lambda_aggregator_unique … := by sorry`). |
| [`Lambda/Allowed_Axioms.lean`](Lambda/Allowed_Axioms.lean) | The axiom allowlist (`propext`, `Quot.sound`, `Classical.choice`). |
| [`.github/workflows/verify-proof.yml`](.github/workflows/verify-proof.yml) | The sole arbiter: `lake build`, no-`sorry` gate, `#print axioms` allowlist check. |
| [`webhook/`](webhook/) | The intake receiver (`intake.py` + JSON Schema) mirrored live at the a11oy Space. |
| [`submissions/`](submissions/) | Submission template + append-only intake receipt ledger. |

## How to win

1. Fork this repo, discharge the `sorry` in `Lambda/Lambda.lean` using **only**
   the allowlisted axioms, and open a PR with the
   [submission template](submissions/SUBMISSION_TEMPLATE.md).
2. `verify-proof` CI runs automatically. **Green = eligible** for the founder-set
   award (published in this repo's pinned issue) + Lean co-author credit.
3. Optionally `POST` your submission metadata to the live intake webhook
   (`https://szlholdings-a11oy.hf.space/api/lambda-bounty/submit`) for a
   hash-chained **Khipu intake receipt**. A receipt acknowledges **intake only** —
   eligibility is still decided solely by `verify-proof` CI on the PR.

## Formal-statement soundness note (read before submitting)

The statement as written conjectures that axioms **A1 idempotence, A2 monotonicity,
A3 symmetry, A4 zero-absorption** pin the aggregator down *uniquely*. Classical
aggregation theory (Aczél 1966; Kolmogorov–Nagumo–de Finetti 1930–31) shows these
four axioms alone are **not** sufficient to single out the geometric mean — e.g.
`min` also satisfies A1–A4 yet differs from the geometric mean. A defensible
*provable* form additionally requires **continuity + bisymmetry/associativity +
homogeneity (or multiplicativity)**, after which the `CAUCHY_ND` step closes. This
is exactly why the problem is published as an **open conjecture under public axiom
audit**, not a theorem. See the deliverable report and `lutar-lean/BOUNTY.md` for
the full discussion; tightening the axiom set is a founder decision.

*Doctrine v11 (749 / 14 / 163 · c7c0ba17) · Λ = Conjecture 1, NOT a theorem.*
