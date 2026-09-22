# Prior-Art Review

**Review date:** 2026-09-21  
**Purpose:** determine which observations are already established and narrow any eventual novelty claim.

## Direct Jev / Jev-like prior art

### TypeSafe: System One Models and Jev
TypeSafe describes Jev as a typed probabilistic decision model with a specialized architecture, parallel sampler, and Reinforcement Learning for Calibrated Decisions (RLCD). This establishes that architecture is only one component of the intended system; training objective and surrounding deterministic software are part of the design story.

- https://typesafe.ai/blog/introducing-system-one-models-and-jev

### Independent Jev calibration audit
The `jev-calibration-audit` already establishes several results that overlap with early observations here: removing an abstain option can catastrophically force a wrong choice; Noul and two-option Choice probabilities can differ materially; Jev itself showed near-zero option-order sensitivity in a 400-item reversal test; bundled hostile neighbor questions produced little interference.

- https://github.com/jujumilk3/jev-calibration-audit
- https://github.com/jujumilk3/jev-calibration-audit/blob/main/FINDINGS.md

**Implication:** abstention importance, formulation sensitivity, and option-order testing are not novel claims from this study. The fact that actual Jev can be more invariant than small Kev is itself important context.

### SemIf / open direct-logit decision readouts
SemIf freezes perturbations including option reversal, criterion paraphrase, irrelevant context, and missing evidence for generation-free direct readouts. Its method explicitly warns that a forced typed output can still be semantically wrong and that softmax over supplied options is conditional on those alternatives rather than operational calibration.

- https://github.com/TheoLeeCJ/SemIf/blob/master/docs/METHOD.md
- https://github.com/TheoLeeCJ/openjev/blob/master/docs/RESULTS.md

**Implication:** irrelevant-context and option-order robustness of generation-free decision readouts are already active prior art. The distinctive part of this study is the matched Kev decision-head decomposition across scale, prompt/schema, source hierarchy, and LoRA interpolation—not the existence of perturbation sensitivity itself.

### Kev's own model cards and research log
Kev already reports strong capacity effects out of domain and publishes option-order flip rates across model sizes. The 0.8B model card explicitly recommends 4B for accuracy and shows a large transfer gap; earlier Kev research states that capacity dominates out-of-domain performance under otherwise similar recipes.

- https://github.com/jaredpalmer/kev/blob/main/docs/model-cards/kev-0.8b.md
- https://github.com/jaredpalmer/kev/blob/main/PLAN.md

**Implication:** "larger Kev is better" is not novel. Our contribution is narrower: on a frozen matched context-robustness matrix, scale changed the *behavioral effect of irrelevant context*, eliminating authoritative-evidence flips while leaving different borderline sensitivities.

## Broader irrelevant-context and prompt-sensitivity literature

### Irrelevant context distractibility
Shi et al. (2023) show that irrelevant context can substantially reduce LLM reasoning accuracy and that explicit instructions to ignore irrelevant information can help but do not define hard isolation.

- https://arxiv.org/abs/2302.00093

### Contextual entrainment and irrelevant-context hallucination
Recent mechanistic and behavioral work shows that irrelevant context can systematically alter logits/predictions rather than acting as random noise.

- Niu et al., *Llama See, Llama Do* (ACL 2025): https://aclanthology.org/2025.acl-long.791/
- Cheng et al., *Stochastic Chameleons* (ACL 2025): https://aclanthology.org/2025.acl-long.1458/

### Spurious social context
Nam & Demszky (2026) directly study spurious social contexts in model-based evaluation and find meaningful prediction shifts; importantly, robustness is not guaranteed by scaling alone in their setting.

- https://arxiv.org/abs/2604.02585

### Pragmatic/context bias and strict prompting
PaCE (ACL Findings 2026) studies context-flip errors and reports that strict prompting can reverse a contextual-sensitivity gap, while scaling alone does not fully remove the phenomenon.

- https://aclanthology.org/2026.findings-acl.959/

### Position sensitivity
Cobbina & Zhou (EMNLP 2025) show that prompt position can change predictions, with smaller models particularly affected in their evaluation.

- https://aclanthology.org/2025.emnlp-main.1503/

## Prior-art conclusion

The broad phenomena observed here—irrelevant-context sensitivity, prompt sensitivity, option-order effects, abstention dependence, and scale effects—are **not new in themselves**.

The most defensible distinctive contribution of this artifact is the **controlled decomposition inside one public Jev-like trained decision-head family**:

- same decision architecture family at 0.8B and 4B;
- matched instruction × option-schema × context matrix;
- source-authority/order controls;
- calibration control;
- option-order controls;
- task-domain controls;
- inference-time LoRA interpolation.

This combination supports a bounded architectural conclusion: generation-free typed decision output is not equivalent to semantic information-flow isolation, and robustness in Kev emerges from the interaction of backbone capacity, decision adaptation, task framing, and option semantics.

No claim of conceptual priority should be made without a deeper literature review if this artifact is developed into a formal paper.
