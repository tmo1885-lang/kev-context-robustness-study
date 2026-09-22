# Claim Boundary

## Supported by this study

1. **Typed output does not imply semantic invariance.** Kev can remain within a fixed choice set while probabilities and, at small scale, selected choices change under irrelevant context, instruction, schema, or order perturbations.
2. **The large failures are strongly scale-dependent in the tested family.** Matched authoritative-evidence flips seen at Kev-0.8B disappeared at Kev-4B in the frozen factorial and targeted 4B controls.
3. **Ambiguous/borderline cases remain context-sensitive at 4B.** Scaling did not create universal invariance.
4. **Instruction and option semantics are part of the decision computation.** Explicit rules and evidence-focused options improved robustness, especially at 0.8B.
5. **Calibration temperature is not the source of the behavioral flips.** Disabling fitted temperature preserved argmax on the frozen subset.
6. **Decision adaptation matters.** LoRA interpolation materially changed the ability to distinguish positive and negative rule cases.
7. **The phenomenon is task-dependent.** Several non-authorization hard-rule controls were highly stable.

## Not supported

- That TypeSafe's **Jev** exhibits the same context failures as Kev-0.8B.
- That Jev-style architecture is uniquely or generally more context-sensitive than generative LLMs.
- That scaling always fixes irrelevant-context bias. The present result is specific to Kev-0.8B → Kev-4B on the frozen tasks.
- That social proof or pressure has a universal direction of effect; direction changed across scale/task/framing.
- That the experiments establish a production security vulnerability or exploit.
- That probabilities from these synthetic cases are validated operational risk estimates.
- That the study identifies a specific transformer circuit or mechanistic cause.
- That direct-decision architecture is equivalent to a deterministic rule engine.
- That the study establishes conceptual priority for context robustness, option-order effects, abstention, prompt sensitivity, or irrelevant-context bias.

## Publication-safe central statement

> In a public Jev-like decision model, typed non-generative output alone did not guarantee semantic invariance. On a frozen matched matrix, Kev-0.8B showed large context-induced decision changes on authoritative authorization evidence, while Kev-4B eliminated those authoritative-evidence flips under the same matrix and targeted controls but retained measurable context sensitivity on borderline cases. Instruction design, option semantics, and decision adaptation materially affected robustness.
