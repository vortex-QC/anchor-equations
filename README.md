# Anchor Equations: An Equation System Beyond Conservation Equality

**Qin Chao** (ORCID 0009-0006-2000-5644 | Juexiao Information Consulting Center, Xingyi 562400, Guizhou, China)

Part of the Constructive Mathematics Series. Companion record to *Anchor Numbers: Completing Dynamic Number with the Anchor Primitive* (doi:10.5281/zenodo.22866459).

## What this record contains

| File | Content |
|---|---|
| `anchor_equations_CN_v1.0.md` | Main document (Chinese) |
| `anchor_equations_EN_v1.0.md` | Main document (English) |
| `AnchorLayer.lean` | Complete Lean 4 formalization (Mathlib base): anchor-sign calculus, evolution engine, flow semigroup, order-type evolution |

## Abstract

Standard mathematics writes equations with the equality sign, and equality is the grammar of conservation: conservation laws are equations, while the *fate* of a dynamic process (convergence, divergence, drift) is invisible inside the equality grammar. This paper elevates destination to a first-class connective: the **anchor equation** `x ⟨anchor T`, joining a left side (the direction of a number: a sequence or orbit) to a right side (an anchor dynamical type: a convergence relation with a uniqueness certificate). The system has three layers: (1) notation and calculus — anchor dynamical types, four calculus rules (all zero-axiom, purely constructive), the empty anchor type giving fate-openness a legitimate equation slot; (2) the evolution engine — reasoning by evolution, not substitution: the time variable enters explicitly (evolution monotonicity, the evolution clock K^m, collectivity, composition rules, the time-lattice bridge — a flow sampled at lattice times *is* discrete iteration, an identity not an analogy — and the full-timeline rate-function version where submultiplicativity of the clock is a corollary, not an assumption); (3) order-type evolution — evolution semantics for non-metric carriers (order preservation as order-collectivity; stationary points as anchors). The anchor sign coincides pointwise with asymptotic notation ~ (Theorem 2.11): anchor equations are not a rival language but the promotion of ~ and → from predicates to operational types. All main theorems are formalized in Lean 4 with zero sorry; the core calculus rules depend on no axioms at all.

## Reproduction

```bash
# Lean 4 with Mathlib; elan install recommended
lake build                 # builds the full project, 8717 jobs
grep -c "sorry" AnchorLayer.lean   # header text only; zero real sorry
```

Every theorem's axiom dependency can be audited with `#print axioms` (see paper, Appendix A).

## Related records

- Anchor Numbers (companion): doi:10.5281/zenodo.22866459
- Statics as Manifestation (dynamic layer): doi:10.5281/zenodo.22785052
- Density Clustering (number layer): doi:10.5281/zenodo.22773691
- Constructive Mathematics Certification Standard v1.3: doi:10.5281/zenodo.22874646

License: CC-BY-4.0.
