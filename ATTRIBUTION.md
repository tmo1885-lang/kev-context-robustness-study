# Attribution and Project Provenance

## Independent study

This repository contains an independent context-robustness study conducted by **Velorin Intelligence**.

The study used **Kev**, a third-party open-source Jev-inspired decision-model project created by **Jared Palmer**.

Velorin Intelligence did not create Kev and is not affiliated with or endorsed by Jared Palmer, the Kev project, TypeSafe, or Jev.

## Original Kev project

**Project:** Kev  
**Author:** Jared Palmer  
**Original repository:** https://github.com/jaredpalmer/kev  
**License:** Apache License 2.0  
**Original license:** https://github.com/jaredpalmer/kev/blob/main/LICENSE

Kev's name is used here descriptively to identify the system tested.

## Relationship to the original project

The experiments reported in this repository were conducted independently using a fork of the public Kev repository.

This standalone repository contains:

- independently produced experimental results;
- analysis of those results;
- research notes;
- claim boundaries;
- prior-art review;
- reproducibility metadata.

It does **not** reproduce the Kev source tree.

It does **not** redistribute Kev model weights, Qwen model weights, training datasets, or third-party software packages.

Readers who wish to use Kev itself should obtain it from the original project and follow the licensing terms provided there.

## Models tested

The frozen study used the following public Kev checkpoints:

- `jaredpalmer/kev-0.8b`
- `jaredpalmer/kev-4b`

Exact model revisions are recorded in `manifest.json`.

These checkpoints use underlying Qwen models and other dependencies whose licensing and terms are controlled by their respective publishers. This repository does not redistribute those assets.

## Jev and TypeSafe

Kev is inspired by TypeSafe's Jev architecture, but **Kev is not Jev**.

The experiments in this repository were performed on Kev.

They should not be interpreted as measurements of TypeSafe's Jev unless explicitly supported by separate evidence.

## Research conclusions

All experimental interpretations, analyses, visualizations, and conclusions in this repository are those of the independent study authors.

They should not be attributed to Jared Palmer, the Kev project, TypeSafe, Qwen, or any other third party unless specifically cited.
