# Results Index

This directory contains the frozen result artifacts used by the Kev Context-Robustness Study. SHA-256 digests and byte sizes are recorded in `manifest.json`.

## Matched scale comparison
- `kev_instruction_schema_context.csv` — Kev-0.8B instruction × option-schema × context factorial.
- `kev4b_instruction_schema_context.json` — matched Kev-4B factorial.
- `kev4b_vs_08b_matched_comparison.csv` — row-aligned 0.8B vs 4B comparison.

## 4B targeted controls
- `kev4b_source_and_option_order_controls.json` — source-authority/order and six-way option-order controls.
- `kev4b_lora_ablation.json` — inference-time LoRA scale control at 0.0, 0.5, and 1.0.
- `kev4b_modal_run_meta.json` — execution and billing metadata for the larger-model run.

## 0.8B context and evidence controls
- `kev_prompt_context_factorial.csv` — prompt × context factorial.
- `kev_robustness_matrix.csv` — broader robustness matrix.
- `kev_negative_evidence_symmetry.csv` — positive/negative authoritative-evidence symmetry.
- `kev_evidence_location_authority.csv` — evidence location and source-authority tests.
- `kev_evidence_strength_curve.csv` — summarized evidence-strength curve.
- `kev_evidence_strength_curve_raw.csv` — raw evidence-strength results.
- `kev_option_label_semantics_raw.csv` — option-label/semantic-form controls.

## Domain controls
- `kev_cross_domain_hard_rules.csv` — tailored hard-rule replication across several non-authorization domains.
- `kev_cross_domain_non_authorization_raw.csv` — additional non-authorization controls.

## Calibration and adaptation controls
- `kev_calibrated_subset.json` — calibrated frozen subset.
- `kev_raw_subset.json` — same subset at raw-logit temperature.
- `kev_lora_scale_0.0.json`
- `kev_lora_scale_0.5.json`
- `kev_lora_scale_1.0.json` — Kev-0.8B LoRA interpolation controls.

## Exploratory control
- `qwen_base_direct_choice_control.json` — exploratory Qwen base direct-choice control; preserved for comparison, not treated as a fully shape-matched replacement for Kev.

Use these files together with `RESEARCH_RECORD.md` and `CLAIM_BOUNDARY.md`. Individual rows should not be generalized beyond the frozen synthetic tasks without additional evidence.
