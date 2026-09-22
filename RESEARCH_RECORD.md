# Kev Context-Robustness Research Record

**Status:** empirical phase frozen for prior-art comparison  
**Date:** 2026-09-21  
**Standalone repository:** `tmo1885-lang/kev-context-robustness-study`  
**Source experiment repository:** `tmo1885-lang/kev`  
**Source experiment branch:** `research/context-robustness`  
**Frozen source commit:** `69cf579a1fdf24998fa9554f2fcadbdd1f354230`  
**Opening Kev base:** `f0ae8fb9af5762254974dcdba8c82cbf48587b2e`  

## 1. Research question

Does a public Jev-like, non-generative decision architecture become semantically invariant simply because it returns typed probability distributions rather than generated text?

Operationally, the study tested whether decisions remained stable when policy-relevant evidence was held fixed while changing: irrelevant context, instruction wording, option semantics, option order, source order, evidence strength, model scale, calibration temperature, and LoRA adaptation strength.

## 2. Systems tested

- **Kev-0.8B** — `jaredpalmer/kev-0.8b`, Hub revision `54f4f8777356cd5bbbb6c6919c657f26e6f2f6d8`; Qwen3.5-0.8B-Base + rank-16 LoRA + pointer head.
- **Kev-4B** — `jaredpalmer/kev-4b`, Hub revision `485ace8703592fcf405488b262449990824cfed1`; same public Kev decision family at larger scale.
- **Qwen base direct-choice control** — exploratory frozen artifact in `results/qwen_base_direct_choice_control.json`; useful as a control, not treated as a fully shape-matched replacement for Kev.

Kev-0.8B ran locally on CPU. Kev-4B inference controls ran on a Modal H100 using the public checkpoint. No model was trained in this study.

## 3. Core experimental structure

The principal matched factorial crossed:

- evidence: `borderline` vs `authoritative`;
- names: Alice vs Ben;
- instruction: generic, strict-record-only, ignore-social, explicit mechanical rule;
- option schema: detailed, terse, policy-focused, evidence-focused;
- context: baseline, neutral filler, social proof, pressure.

That produces 256 matched decisions per model. Additional bounded controls tested calibration, option permutations, source hierarchy/order, evidence strength, polarity symmetry, cross-domain hard rules, and LoRA scale.

## 4. Main matched scale result

Expected label for borderline evidence was `unknown`; expected label for authoritative positive evidence was `allow`.

| Evidence | Context | Kev-0.8B correct | Kev-4B correct |
|---|---:|---:|---:|
| borderline | baseline | 17/32 | 28/32 |
| borderline | neutral | 20/32 | 28/32 |
| borderline | social proof | 30/32 | 19/32 |
| borderline | pressure | 32/32 | 29/32 |
| authoritative | baseline | 32/32 | 32/32 |
| authoritative | neutral | 32/32 | 32/32 |
| authoritative | social proof | 4/32 | 32/32 |
| authoritative | pressure | 8/32 | 32/32 |

Relative to each cell's own baseline decision, authoritative-evidence flip rates were 87.5% / 75.0% for social proof / pressure at 0.8B and 0% / 0% at 4B.

Mean change in `P(allow)` under authoritative evidence was −0.424 / −0.381 at 0.8B and −0.020 / −0.059 at 4B for social proof / pressure.

The two models agreed on only 163/256 (63.7%) selected choices in the matched factorial, so scale changed the behavioral surface substantially rather than merely sharpening the same answers.

## 5. Prompt and schema effects

At 0.8B, both instruction wording and option descriptions materially affected the distribution. A descriptive balanced decomposition of `P(allow)` found context to be the largest source of variation, with instruction and schema also contributing and interacting with context. This is descriptive for the frozen synthetic matrix, not a population-level ANOVA.

Explicit mechanical instructions plus evidence-focused option definitions greatly improved decision-boundary robustness, but did not make probabilities invariant. The appropriate interpretation is **robust readout, not hard information-flow isolation**.

At 4B, authoritative evidence was stable across the matched instruction/schema matrix, while borderline cases retained context sensitivity, especially to social proof.

## 6. Option-order control

Kev-0.8B showed option-order sensitivity in several three-option authorization cases; even an authoritative positive case could change under generic wording. Explicit rule + evidence-focused options improved but did not eliminate borderline order sensitivity.

Kev-4B, under the matched explicit-rule/evidence-focused control, was stable in all 42 tested permutations (7 states × 6 option orders). Probability spreads were small and no argmax changed.

This does not contradict Kev's own published aggregate option-order flip rates; our control is a small targeted subset under one robust prompt/schema configuration.

## 7. Source authority and order

In the 0.8B source-order replication, authoritative truth was followed in 62/64 conflicting-source cases. Both failures occurred when a non-authoritative roster asserted a negative status and the authoritative positive record appeared later.

The matched 4B control followed the authoritative source in **64/64** cases across positive/negative truth, authoritative-first/last order, four names, and four weak-source forms (roster, coworker, old note, chat). Thus the 0.8B source-order failures did not survive scaling in this test.

## 8. Evidence polarity symmetry

With tailored explicit rules, authoritative `deny` evidence at 0.8B was more resistant to irrelevant context than authoritative `allow` evidence. Social proof flipped 2/6 authoritative-allow cases and 0/6 authoritative-deny cases across config/finance/deployment in the frozen symmetry matrix.

At 4B, the matched hard-rule mirror stayed correct for both polarities under baseline, neutral, social-proof, and pressure contexts, with mean expected-class probabilities around 0.98–0.99.

## 9. Calibration control

A frozen subset was rerun with `KEV_TEMPERATURE=1.0`. All selected choices were unchanged. Removing temperature calibration sharpened probability margins rather than changing the argmax. Therefore the observed context-driven choice changes cannot be attributed merely to temperature calibration.

## 10. Evidence-strength curve

The 0.8B explicit-rule curve did not form a clean monotonic hierarchy from self-claim → weak source → stale record → current summary → authoritative record. Semantic form mattered: for example, self-claims and non-authoritative rosters could sometimes receive more weight than their source status warranted, while stale authoritative evidence often moved toward `unknown`.

The correct interpretation is not that Kev lacks the concept of source authority; rather, smaller-model readout can let semantic form compete with declared source status.

## 11. Cross-domain controls

Tailored hard-rule tests on return windows, warranty coverage, membership discounts, event tickets, and additional non-authorization classifications were substantially more robust than the fragile 0.8B authorization cases. This rules out a broad claim that irrelevant social context necessarily destabilizes every Kev decision.

Task semantics matter. Authorization-like judgments appear especially vulnerable at small scale, plausibly because trust, legitimacy, pressure, and social approval are semantically adjacent to the decision domain. This study does not establish the mechanism.

## 12. LoRA adaptation ablation

`KEV_LORA_SCALE` was used as an inference-time interpolation control.

For Kev-4B, scale `0.0` did not provide a competent symmetric authorization classifier: positive cases often looked plausible while authoritative negative cases were frequently read as `allow` or `unknown`. By scale `0.5`, the frozen positive/negative subset was already highly accurate and context-robust; scale `1.0` remained strong.

This supports the limited causal statement that Kev's decision adaptation materially contributes to the observed decision behavior; the trained pointer head is not simply exposing a complete classifier that already exists in the unadapted backbone.

The 0.8B LoRA ablation likewise showed material adaptation effects but substantially more fragility than the 4B ablation.

## 13. Null and negative results

- Repeating an identical simple request produced identical probabilities in the local Kev-0.8B serving configuration.
- Packed vs separate question execution produced matching answers in the tested case, consistent with Kev's intended question isolation.
- Neutral filler usually produced much smaller shifts than semantically loaded social-proof/pressure text.
- Several non-authorization hard-rule domains showed essentially no behavioral effect from the tested social context.
- The large 0.8B authoritative-evidence failures did **not** reproduce at 4B.

These negative results are part of the finding and should not be omitted from any write-up.

## 14. Interpretation

The most defensible architectural synthesis is:

> **A typed non-generative decision head constrains the output space; it does not by itself constrain the evidence space.**

Kev cannot wander into prose or invent a fourth choice, but the transformer still builds a contextual representation from the state, instructions, and option semantics. At small scale, irrelevant semantic cues can materially alter that representation/readout. Larger capacity and decision adaptation can make hard-evidence cases dramatically more robust, without making every ambiguous case invariant.

Therefore these experiments do not support treating a neural decision model as a deterministic rule engine. Where an application requires hard exclusion of irrelevant inputs or mechanically enforceable source precedence, deterministic software remains the stronger enforcement mechanism.

## 15. Reproducibility and preservation

All result artifacts are preserved under `results/` and hashed in `manifest.json`. This standalone repository was assembled from the frozen source artifact at commit `69cf579a1fdf24998fa9554f2fcadbdd1f354230`. The 4B run metadata records Modal execution context and observed workspace billing. The upstream `jaredpalmer/kev` repository was never used as a write target; experiments were performed in an independent fork.
