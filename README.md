# Kev Context-Robustness Study

An independent study of context robustness in **Kev**, an open-source Jev-inspired decision model.

**Status:** Frozen experimental record  
**Study date:** September 2026  
**Conducted by:** Velorin Intelligence

## Research question

If a neural decision model is restricted to a fixed set of typed answers rather than generating free-form text, does that also make its judgment insensitive to irrelevant context?

In short: **not by architecture alone.**

Across a controlled set of experiments, Kev's probabilities—and at smaller scale, sometimes its selected decisions—changed when policy-relevant evidence was held fixed while instructions, option definitions, irrelevant social context, source order, or option order changed.

The strongest qualification was model scale.

On a matched authoritative-evidence matrix:

| Perturbation | Kev-0.8B decision flips | Kev-4B decision flips |
| --- | ---: | ---: |
| Neutral filler | 0 / 32 | 0 / 32 |
| Social proof | 28 / 32 | 0 / 32 |
| Pressure | 24 / 32 | 0 / 32 |

The large failures observed at 0.8B therefore did **not** appear to be an unavoidable property of the decision architecture.

Kev-4B was not universally context-invariant, however. On deliberately borderline evidence, social proof still changed 9/32 matched decisions and pressure changed 3/32.

## Practical interpretation

> **Typed decision heads constrain the output space. They do not, by themselves, constrain the evidence space.**

The experiments suggest that robustness in this decision architecture depends on the interaction of:

- backbone capability;
- decision adaptation;
- instruction design;
- option semantics;
- task structure;
- input context.

For systems engineering, that supports a distinction between **bounded neural judgment** and **deterministic authority**.

## What this study does not claim

This study does **not** establish that:

- TypeSafe's Jev has the same failures observed in Kev-0.8B;
- Jev-style models are uniquely vulnerable to irrelevant context;
- scaling generally eliminates contextual bias;
- these synthetic experiments demonstrate a production security vulnerability;
- the broad phenomena of prompt sensitivity, abstention, option-order effects, or irrelevant-context sensitivity are novel.

See [`CLAIM_BOUNDARY.md`](CLAIM_BOUNDARY.md) for the complete claim boundary.

## Repository contents

- [`RESEARCH_RECORD.md`](RESEARCH_RECORD.md) — frozen methodology, controls, results, and interpretation
- [`CLAIM_BOUNDARY.md`](CLAIM_BOUNDARY.md) — supported and unsupported claims
- [`PRIOR_ART.md`](PRIOR_ART.md) — comparison with relevant prior work
- [`ATTRIBUTION.md`](ATTRIBUTION.md) — project provenance and third-party attribution
- `CITATION.cff` — citation metadata
- `manifest.json` — frozen model revisions and hashes of result artifacts
- `results/` — raw and matched experimental results

## Project provenance

**Kev is not a Velorin Intelligence project.**

Kev is an open-source Jev-inspired decision-model project by **Jared Palmer**, distributed under the Apache License 2.0.

Original project:  
https://github.com/jaredpalmer/kev

Original Kev license:  
https://github.com/jaredpalmer/kev/blob/main/LICENSE

The experiments and analysis in this repository were conducted independently by Velorin Intelligence using a fork of the public Kev repository.

Velorin Intelligence is not affiliated with or endorsed by Jared Palmer, the Kev project, TypeSafe, or Jev.

## Reproducibility

The frozen study records exact Kev model revisions and preserves the raw result artifacts used in the analysis. Larger-model inference controls were run on a Modal H100; no models were trained as part of this study.

The original Kev source code is **not** reproduced in this standalone repository.
