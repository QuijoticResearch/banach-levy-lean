# Operator Factorization Beyond Hilbert Spaces

Lean 4 / Mathlib formalization of:

> R. Fontes, "Operator Factorization Beyond Hilbert Spaces: Representability Obstructions and Leibniz Defects for Stable Levy Processes," Quijotic Research, 2026.

**2,499 lines. 0 sorry. 0 axioms.**

## What This Formalizes

The paper develops stochastic calculus for symmetric stable Levy processes in Banach space, proving three main theorems:

- **Theorem A (Fluctuation Factorization):** Under hypotheses (H1)-(H4), centered functionals factor through the divergence operator.
- **Theorem B (Product Rule with Jump Defect):** The Leibniz defect captures the jump correction to the product rule.
- **Theorem C (Chaos Characterization):** The Poisson chaos expansion identifies ker(D) and im(delta) via truncation.

The formalization also constructs the Poisson infrastructure and Levy-Ito decomposition from first principles, deriving (not axiomatizing) the compensated integral properties from compound Poisson finite sums.

## Architecture

The file `BanachLevyComplete.lean` has three parts:

| Part | Lines | Content |
|------|-------|---------|
| **1. Poisson Infrastructure** | ~350 | Stable density, Poisson mean/variance (proved via HasSum), canonical construction |
| **2. Levy-Ito Framework** | ~850 | Finite telescoping, compensated integral construction, L2 convergence, Poisson chaos orthogonality, compound Poisson path |
| **3. Banach Energy Space** | ~1,200 | Abstract framework, fluctuation factorization, representability obstruction, product rule, chaos characterization, stable instantiation |

## Key Results

### Proved from scratch (pure algebra / real analysis)
- `poisson_mean_identity` -- E[Poisson(r)] = r (HasSum proof)
- `poisson_variance_identity` -- Var(Poisson(r)) = r (three HasSum instances combined)
- `finite_telescope` -- compound Poisson Ito formula = finite sum (Finset.sum_range_sub)
- `first_chaos_orthogonal` -- Poisson chaos orthogonality (tsum_mul_left)
- `l2_cauchy_vanishes` -- L2 Cauchy estimate for double truncation (rpow continuity)
- `product_ito_paired_derived` -- product Ito formula derived from decomposition

### Constructed (not axiomatized)
- `BanachEnergySpace.D` -- operator-covariant derivative, constructed via mk_dual
- `ConcreteStableJumpCount.G0_poisson` -- Poisson distribution by Measure.map_id
- `ConstructedCompensatedIntegral.toAxioms` -- bridge from finite-sum construction to axiom interface
- `compound_poisson_path` -- concrete cadlag path as a finite sum with indicators

### Main theorems
- `BanachEnergySpace.fluctuation_factorization` -- Theorem A
- `BanachEnergySpace.product_rule_with_jump_defect` -- Theorem B
- `BanachEnergySpace.chaos_kernel_characterization` -- Theorem C
- `stable_levy_obstruction` -- representability obstruction for stable processes

## Blueprint

The dependency graph is available at: https://quijoticresearch.github.io/banach-levy-lean/blueprint/

## Building

Requires Lean 4 (v4.28.0) and Mathlib.

```bash
lake exe cache get   # download Mathlib oleans
lake build BanachLevyComplete
```

To verify the blueprint declarations:
```bash
lake build checkdecls
lake exe checkdecls blueprint/lean_decls
```

## Companion Formalization

The Hilbert-space paper ("The Operator Derivative in Continuous Stochastic Calculus") is formalized separately in `OperatorDerivative.lean` (~5,200 lines, 0 sorry, 1 axiom). The Banach framework generalizes the Hilbert one: when H_X is Hilbert, the Leibniz defect vanishes (`HilbertEnergyData.leibniz_defect_vanishes`).

## License

Apache 2.0
