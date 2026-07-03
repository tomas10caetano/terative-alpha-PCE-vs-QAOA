# Iterative-α Pauli Correlation Encoding for Noisy Combinatorial Optimization

Benchmarking a qubit-efficient encoding (PCE) against QAOA for MaxCut, 
showing that under hardware noise a 4-qubit PCE circuit outperforms a 
15-qubit QAOA — because shallower circuits accumulate less error.

## Key result

Under an `ibm_fez`-derived noise model, Iterative-α PCE encoding 15 graph 
nodes into **4 qubits** consistently beats QAOA using **15 qubits** 
(e.g. cut 142 vs 89, 15-node graph). The advantage is structural: QAOA's 
one-qubit-per-node encoding transpiles to high circuit depth (SWAP 
overhead), which noise degrades severely, while PCE's compressed circuit 
stays shallow.

Two mechanisms drive the gap:
- **Circuit compression** → less depth → smaller noise exposure surface.
- **Progressive binarization** (the iterative-α scheme) → pushes 
  expectation values away from zero → protects the sign readout against 
  shot-noise variance (σ ≈ 1/√N_s ≈ 0.022 at 2048 shots).

## Method

Three methods compared, in noiseless (statevector) and noisy simulation, 
on 10- and 15-node graphs:

| Method | Qubits (15 nodes) | α schedule | Optimizer |
|---|---|---|---|
| QAOA | 15 | — | COBYLA |
| Standard PCE | 4 | fixed | COBYLA |
| Iterative-α PCE | 4 | progressive (Alg. 1) | COBYLA + warm restart |

[breve explicação do encoding: nós → correlações de Pauli XX/YY/ZZ, 
3·C(m,2) ≥ n_nodes]

## Repository structure
[lista dos ficheiros: notebook, relatório, etc.]

## Reference
Padín-Martínez et al. (2026), arXiv:2602.17479 — the PCE method this 
work benchmarks and extends.

## Context
Undergraduate research project (Engineering Physics, FCUP/FEUP Porto), 
supervised at INESC TEC.

## Status & caveats
Exploratory benchmark. The optimization budget is not matched across 
methods (Iterative-α runs more evaluations); see the report's 
methodology note. Circuit-depth measurements and a PCE-specific ansatz 
are planned extensions.
