# Geometry-Topology-Coequal-Framework-GTCF-
A mathematical and computational framework unifying geometry, topology, and persistent homology for structural comparison of proteins and other complex 3D objects.
# GTCF Section 6 Verification Scripts

## Status
- `gtcf_core.py` — the core G/T computation functions (bend angle, persistent homology, bottleneck distance). VALIDATED.
- `smoke_test.py` — runs the pipeline on synthetic data with a known 13-degree bend. VALIDATED: correctly reproduces the Structural Blindness pattern (G differs ~13deg, T bottleneck distances ~0).
- `run_verification.py` — the real pipeline for 1JFF/1SA0 (Theorem 1) and 4JQO/3KZK (Theorem 2). NOT YET RUN on real data — requires internet access to files.rcsb.org, which this sandbox's egress proxy blocks (confirmed: HTTP 403 Forbidden).

## To actually complete Theorem 1/2 verification
Run on any machine with internet access:

```bash
pip install biopython ripser persim numpy scipy
python run_verification.py
```

This will download 1JFF, 1SA0, 4JQO, 3KZK directly from RCSB, compute:
- G (bend angle) and T (persistence diagram) for the tubulin pair
- G (radius of gyration) and T (persistence diagram) for the knot pair

and print the bottleneck distances needed to confirm or refute the
paper's conditional theorems with real numbers.

## Known limitation flagged in the script
Standard Vietoris-Rips persistent homology on a raw Calpha point cloud
does not directly detect knot type. For Theorem 2, treat this script's
output as a supplementary geometric signal only — the primary evidence
should still be the published knot-detection result cited in the paper
(the Royal Society Interface persistence-landscape study on 3KZK/4JQO).
