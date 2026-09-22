# v1.0.0 — Frozen Research Artifact

This release freezes the initial Kev Context-Robustness Study.

## Included

- matched Kev-0.8B and Kev-4B instruction × option-schema × context experiments;
- source-authority and option-order controls;
- calibration and evidence-strength controls;
- cross-domain hard-rule controls;
- LoRA interpolation controls;
- prior-art review;
- explicit claim boundary;
- project attribution and provenance;
- SHA-256 manifest for all 21 frozen result artifacts.

## Central finding

> Typed decision heads constrain the output space. They do not, by themselves, constrain the evidence space.

On the frozen authoritative-evidence matrix, Kev-0.8B showed large context-induced decision changes under social proof and pressure, while Kev-4B eliminated those authoritative-evidence flips under the matched matrix and targeted controls. Borderline cases remained measurably context-sensitive.

## Scope

This release reports experiments on **Kev**, an open-source Jev-inspired decision model by Jared Palmer. It does **not** report direct testing of TypeSafe's Jev.

See `CLAIM_BOUNDARY.md` for the complete supported/unsupported claim boundary and `ATTRIBUTION.md` for project provenance.

## License

Original material in this repository is licensed under **CC BY 4.0**, subject to the scope and third-party exclusions in `LICENSE_SCOPE.md`.

## Frozen provenance

Source experiment repository: `tmo1885-lang/kev`  
Source experiment branch: `research/context-robustness`  
Frozen source commit: `69cf579a1fdf24998fa9554f2fcadbdd1f354230`
