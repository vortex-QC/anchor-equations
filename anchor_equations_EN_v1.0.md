# Anchor Equations: An Equation System Beyond Conservation Equality

**Qin Chao** (ORCID 0009-0006-2000-5644 | Juexiao Information Consulting Center, Xingyi 562400, Guizhou, China)

**Abstract**: Equations in standard mathematics are joined by the equals sign, and the equals sign is the grammar of conservation — conservation laws are equalities, and the "where-to" of dynamics (convergence, divergence, drift) can appear within conservation equalities only in the derivative form of rates of change, while the limiting fate of a process is invisible to the grammar of the equals sign. The sister work [2] completed the dynamic ontology of numbers with the anchor primitive, but its destination relations remain scattered across the theorems in predicate form. This paper promotes destination to a **first-class connective of equations**: the anchor equations — a non-conservation equation that joins a left component (the direction of numbers: a sequence or orbit) to a right component (an anchor dynamical type: a convergence relation plus a destination-uniqueness certificate) via the anchor sign x ⟨anchor T. The system has three layers: (1) the notation-and-calculus layer — anchor dynamical types, anchor-sign notation, and four calculus rules (readout / type monotonicity / agreement of joint solutions / empty anchor type), where the empty anchor type gives "fate-open" (drifting without end) a legitimate right-hand position in an equation; (2) the evolution engine layer — reasoning uses not substitution but evolution: the time variable enters explicitly; five theorems covering evolution monotonicity, evolution rate (the K^m evolution clock), and evolution collectivity, plus composition rules (series evolution multiplies rates / clock addition), plus the time-lattice bridge of the flow semigroup (lattice-point sampling of the flow = discrete iteration, an identity, not an analogy) and the full-timeline rate-function version (the clock's submultiplicativity is a corollary, not an assumption); (3) the order-type evolution layer — the evolution semantics of non-metric carriers: the order-convergence anchor sign, order preservation under evolution (order collectivity), and the stationary point theorem (an anchor is where evolution stops). The anchor sign coincides strictly with the standard asymptotic notation (Theorem 2.11: convergence ⟺ dist→0), so the anchor equations are not a fresh start: they promote ~ and → from predicates to operable types. All main theorems have a Lean 4 formalization (zero sorry, Appendix A), and the core calculus rules have zero axiom dependence (pure construction).

---

## §1 Introduction

### 1.1 The Equals Sign Is the Grammar of Conservation

The equation language of standard mathematics grows around the equals sign. The core fact written by the equals sign is conservation: conservation of mass, of energy, of charge — every conservation law is an equality; this is the linguistic facet of Noether's theorem: **symmetries give conserved quantities, and conserved quantities are written as equalities**. The equations of motion are also equalities (F=ma), but their equals sign joins instantaneous quantities — a dynamical process is chopped into infinitely many instants by the grammar of the equals sign, and the **overall fate** of the process (where this orbit ultimately goes, whether it ever stops) appears in none of the individual equalities: fate is a limit statement, and limit statements are second-class citizens (they require writing lim in addition, and the right side of lim is still an equals sign).

The sister work [2] diagnosed the silence of the dynamic axioms of numbers on destination (Anchor Numbers, Theorem 3.1: two legitimate models of the same autonomous dynamics with opposite destinations) and completed it with the anchor primitive. But the destination relations of that completion remain scattered across the theorems in predicate form (Stabilizes, Tendsto, Completion collapse) — **destination does not yet have its own grammar**. This paper adds that layer: promoting the destination relation to a first-class connective of equations.

Founder seed (verbatim anchor in Appendix B.1): where standard mathematics starts from various conservations and writes equalities, starting from the dynamic nature of numbers one can write the anchor sign — the left side is the direction of numbers, the middle is the anchor sign (not an equals sign, nor a greater-than or less-than sign), and the right side is a description of an anchor dynamical type. This paper formalizes that proposal and proves that it naturally grows a complete calculus and engine.

### 1.2 The Historical Position of the Connective

The family of connectives in the history of mathematical notation:

| Connective | Semantics | Relation to the anchor sign |
|---|---|---|
| = | numerical equality / conservation | the grammar of conservation; the anchor sign does not replace it |
| ~ | asymptotic equivalence / distributed-as | **the nearest precedent**: type membership, not numerical equality; the anchor sign and ~ coincide pointwise on the completion type (Theorem 2.11) — the anchor sign is a strict generalization of ~ |
| → | convergence / limit | writable only once fate is already settled; the anchor sign brings "whether it converges" into type eligibility |
| categorical arrows | morphisms between objects | between objects, not within equations; the anchor sign is a destination connective within equations |
| ≤/< | order relations | the convergence semantics of order-type anchor signs falls on orders (§3.5), but the anchor sign itself is not an order relation |

The Leibniz–Newton dispute was a dispute over **notation for quantities** (the dx notation), not over **connectives** — extensions at the connective level (~, →) have historical precedents, but none promoted destination to a type with a functionality certificate. Positioning of the anchor sign: a unified generalization of ~ and →, promoting destination from a derivative statement to a first-class connective.

### 1.3 Contributions of This Paper

1. **Anchor-sign calculus** (§2): the anchor dynamical type (a convergence relation plus a destination-uniqueness certificate — destination uniqueness moves from a proof obligation into type eligibility), anchor-sign notation, four calculus rules all with zero axiom dependence (pure construction); three typed anchor instances with mutually exclusive mechanisms (metric type / completion type / lattice-order type), plus the equivalence theorem between the anchor sign and the asymptotic notation (Theorem 2.11);
2. **The evolution engine** (§3): reasoning uses not substitution but evolution — the time variable enters explicitly; five theorems (monotonicity / rate / collectivity, etc.) plus composition rules (composition law / clock addition / alternating collectivity), plus the time-lattice bridge of the flow semigroup (Theorem 3.10: φ.flow(n·t₀)=(φ t₀)^[n]) and the full-timeline rate-function version (the clock's submultiplicativity is a corollary, Theorem 3.11); order-type evolution (order preservation / stationary points) supplies the evolution semantics for non-metric carriers;
3. **The equation-system reading** (§4): the empty anchor type = the equation form of fate-openness; solving an anchor-sign equation = finding the destination (a systematic contrast with solving an equality equation = finding the conserved quantity); the anchor-sign equation is the syntactic upgrade of standard mathematics' limit notation (the equals sign to the right of lim).

### 1.4 Scope Statement

The system of this paper is self-contained within the standard language of metric spaces and order theory; no acceptance of any background of this framework is presumed. The anchor equations are the notation-calculus layer of anchor numbers [2], not a new member of constructive mathematics; the generator characterization of continuous-time evolution (Hille–Yosida-level theory) is outside the domain, and the parametrization of clock functions is an open problem (§6.2).

## §2 Anchor-Sign Calculus: Definitions and Rules

### 2.1 The Anchor Dynamical Type

**Definition 2.1 (anchor dynamical type).** An anchor dynamical type T on a universe α consists of two parts:
- a convergence relation Sub : α^ℕ → α → Prop — "the sequence x is T-converged to the destination point p";
- a functionality certificate unique: destinations of convergence of the same sequence under the same type are unique (Sub x p → Sub x q → p = q).

The functionality certificate is the design core of this definition: it moves "destination uniqueness" from a proof obligation of each theorem into type eligibility — only convergence relations with unique destinations are eligible to stand to the right of the anchor sign, and their destination points can therefore be referenced, transported, and jointly solved like right-hand terms of the equals sign. **This is the foundation of the anchor-sign counterpart of the substitution rule**.

**Definition 2.2 (anchor sign).** x ⟨anchor T :⇔ ∃ p, T.Sub x p — the sequence x is anchor-converged by the type T (to some destination point).

### 2.2 Four Calculus Rules (All Zero-Axiom, Pure Construction)

**Rule 1 (readout).** x ⟨anchor T ⟹ ∃ p, T.Sub x p — when the anchor sign holds, the destination point can be extracted, and from then on the right of the anchor sign can be referenced like an object of the equals sign.
**Rule 2 (type monotonicity).** containment of convergence relations (T ⊆ T') ⟹ x ⟨anchor T ⟹ x ⟨anchor T' — converged by the weaker anchor type implies converged by the stronger anchor type.
**Rule 3 (agreement of joint solutions).** T ⊆ T' and T.Sub x p, T'.Sub x q ⟹ p = q — when the same sequence is converged by both types simultaneously, the destinations agree: the anchor-sign counterpart of the agreement of joint solutions for equalities.
**Rule 4 (empty anchor type).** Under the empty anchor type (Sub constantly false) the anchor sign is constantly false: ¬(x ⟨anchor empty anchor type).

Rule 4 is this system's grammatical stance on the ontology of dynamics: what "drift ⟨anchor no-anchor" writes is not a holding equation but a non-holding equation — "no anchor" does not mean "anchored to an empty object"; the destination predicate itself is false. Fate-openness (drifting without end) thereby acquires a legitimate right-hand position in an equation: it can be written, jointly solved, and reasoned about — it simply does not hold. This is exactly the grammatical-layer resolution of the incompleteness diagnosis of anchor numbers [2] (D0's silence on destination): the grammar of the equals sign cannot hold fate, and the grammar of the anchor sign assigns fate a position — including "no fate".

### 2.3 The Three Typed Anchor Signs

The three typed instances are mechanistically disjoint, each carrying one line of destination mechanism:

**Definition 2.3 (metric type).** metricType(f): Sub x p := x is the f-orbit of some starting point and converges topologically to p (on ℝ, T2 guarantees functionality). Introduction piece (Theorem 2.4): every orbit of a Banach contraction mapping [9] is ⟨anchor metric type.

**Definition 2.5 (completion type).** completionType: Sub x p := x converges topologically to p. Introduction piece (Theorem 2.6): Cauchy sequences ⟨anchor completion type (completeness of the reals = the static-side form of the anchor [2], Theorem 3.12). Contrast piece (Theorem 2.7): the +1 drift on ℝ is not converged by the completion type — a concrete instance of the empty anchor type.

**Definition 2.8 (lattice-order type).** orderType(f) (f a monotone operator on a complete lattice): Sub x p := x is the f-iteration orbit of some starting point and p = the supremum of the orbit — **order-convergence semantics**. Functionality is guaranteed by the starting point being uniquely determined by the first term of the sequence (x 0 = f^[0] x₀ = x₀); the introduction piece is zero-axiom (Theorem 2.9). Interface piece (Theorem 2.10): the Tarski-Knaster least fixed point [10][11], as a constant orbit, is converged by the lattice-order type (the least fixed point is determined endogenously by the lattice structure). Honest boundary: without assuming ω-continuity, the iterated supremum need not be a fixed point — this system claims only the convergence structure; existence of fixed points is carried separately by the Tarski theorem.

**The significance of the three types standing side by side**: the metric type carries evolution (§3), the completion type carries the anchor collapse [2], and the lattice-order type carries the fixed-point mechanism — three lines of destination mechanism written uniformly under the grammar of the anchor sign.

### 2.4 The Anchor Sign and the Asymptotic Notation: Theoremization of a Strict Generalization

**Theorem 2.11 (pointwise coincidence with ~).** completionType.Sub x p ⟺ dist(x n, p) → 0 — anchor-sign convergence and the standard asymptotic language coincide in both directions.

The anchor sign is not a fresh start: on the completion type it is semantically identical to ~. The difference lies in grammatical status — ~ is a predicate (a relational notation between statements), while the anchor sign is a type with a functionality certificate (the destination can be referenced, jointly solved, and can take part in type-monotonicity reasoning). Theorem 2.11 guarantees that this upgrade loses nothing: every convergence statement writable with ~ is writable with the anchor sign, and conversely; the anchor sign additionally gains the empty anchor type (fate-openness) and operations on the type lattice.

## §3 The Evolution Engine: Reasoning with the Time Variable

### 3.1 Engine Choice: Substitution vs. Evolution

The reasoning engine of equality equations is **substitution**: the two sides of an equality can be substituted for each other, with information unchanged. Founder seed (verbatim anchor in Appendix B.2): since the anchor equations are a representation of the dynamic ontology of numbers, they should use evolution, introducing the time variable — substitution is a spatial term transformation (the conservation engine of the equals sign; time does not flow), while evolution is a temporal advancement of state (the destination engine of the anchor sign; each step tightens, and information tends toward determination). Every theorem of this section is proved by induction on time, and not one substitution appears in the proofs: **the reasoning engine = the advancement of time itself**. This is not rhetoric: the engine choice is a developer of the ontology — substitution calculus is the engine of static objects; evolution calculus is the engine of the moving ontology.

### 3.2 The Five Theorems of Evolution

Let f be a contraction mapping with fixed point p on a metric space (ContractingWith K f, K<1) [9]:

**Theorem 3.1 (single-step tightening).** edist(f z, p) ≤ edist(z, p) — each step of evolution tightens, with no loop back.
**Theorem 3.2 (evolution monotonicity).** n ≤ m ⟹ edist(f^[m] x, p) ≤ edist(f^[n] x, p) — the orbit's distance to the destination is monotone non-increasing in time; reasoning = reading out time constraints.
**Theorem 3.3 (evolution rate).** edist(f^[m] x, p) ≤ K^m · edist(x, p) — **K^m is the evolution clock**: the time variable enters the quantitative bound; m steps of evolution compress the error by a factor of K^m.
**Theorem 3.4 (evolution collectivity).** edist(f^[m] x, f^[m] y) ≤ K^m · edist(x, y) — different starting points are drawn together by the same evolution; evolution is collective behavior and requires no fixed point.

### 3.3 Composition Rules

**Theorem 3.5 (evolution composition law).** f K-contraction, g L-contraction ⟹ f∘g is a (K·L)-contraction — evolution in series, rates multiply. This is the evolution engine's counterpart of the substitution engine's "transitivity".
**Theorem 3.6 (evolution clock addition).** edist(f^[m+n] x, p) ≤ K^(m+n)·edist(x, p) — the time variable obeys an addition law; the evolution clock keeps accounts by the exponential law.
**Theorem 3.7 (alternating evolution collectivity).** Alternating g first and then f for m rounds, the distance between the two orbits is ≤ (K·L)^m·the initial distance (honest annotation: (f∘g)^[m] is alternating evolution, not f^[m]∘g^[m]).
**Theorem 3.8 (ternary composition law and the composite clock).** The composition rules close under n-ary composition: three steps in series multiply rates; the clock for the alternating composition evolving to the fixed point = (K·L)^n.

Interface piece: every orbit of the composite contraction mapping carries its anchor type (⟨anchor metric type(f∘g)) — **every alternating orbit of the evolution engine is a legitimate left component of an anchor-sign equation**.

### 3.4 The Flow Semigroup and the Time-Lattice Bridge

**Definition 3.9 (flow semigroup).** flow : ℝ → X → X satisfies flow 0 = id and flow(s+t) = flow s ∘ flow t — the time variable itself forms an additive semigroup; evolution composes by time shifts.

**Theorem 3.10 (time-lattice bridge).** φ.flow(n·t₀) x = (φ.flow t₀)^[n] x — the flow at integer-multiple instants is exactly the discrete iteration of the generating map.

The meaning of the bridge: the docking point between continuous-time dynamical processes and the evolution engine is theorematized — **lattice-point sampling of the flow = discrete iteration, an identity, not an analogy** (given directly by induction on the semigroup law). The three laws of evolution monotonicity, clock, and collectivity hold verbatim on flows via the time-lattice bridge (Corollaries 3.10a-c).

**Full-timeline generalization (rate-function version)**: without assuming contraction at every instant, let a rate function c : ℝ → ℝ≥0∞ (c(t)-Lipschitz at each instant) — this is **the axiomatization of the evolution clock** (discrete K^m and continuous e^{−λt} are both special cases of c):

**Theorem 3.11 (clock addition is a corollary).** c(s+t) ≤ c(s)·c(t) need not be assumed — it is derived for free from the semigroup law plus per-instant Lipschitzness.
**Theorem 3.12 (full-timeline evolution monotonicity).** t ≤ s ⟹ edist(φ s x, p) ≤ edist(φ t x, p) — the core step is the semigroup decomposition s = t + (s−t).

### 3.5 Order-Type Evolution: Non-Metric Carriers

Evolution on a lattice has no distance, but it has order. Order-type evolution supplies the evolution semantics for non-metric carriers:

**Theorem 3.13 (order-type evolution monotonicity).** The iteration orbit of an apex start (f x₀ ≤ x₀) is antitone in the order — evolution in the order tightens at every step, with no loop back; the proof contains only order induction and monotonicity, zero metric structure, exactly isomorphic to Theorem 3.2.
**Theorem 3.14 (order version of collectivity = order preservation under evolution).** x ≤ y ⟹ f^[n] x ≤ f^[n] y (zero axioms) — **metric collectivity tightens distance; order collectivity preserves structure**: the correct form of "drawing together" in the order is not shrinking distance but invariance of the order relation.
**Theorem 3.15 (stationary point = anchor).** A step that stands still in the order (f^[n+1] x₀ = f^[n] x₀) is a fixed point — an anchor is where evolution stops. This echoes the D0 diagnosis of anchor numbers [2]: unanchored evolution may never stop; once anchored, the stationary point is the destination.

## §4 The Crown: Anchor Equations as an Equation System

### 4.1 The Division of Labor between Two Kinds of Equations

| | Equality equations | Anchor-sign equations |
|---|---|---|
| Connective semantics | conservation / equality | destination / convergence |
| Right-hand term | conserved quantity | anchor dynamical type |
| Reasoning engine | substitution (information unchanged) | evolution (information tends toward determination) |
| Solving the equation | find the value of a conserved quantity | find the destination of an orbit |
| Form of non-holding | contradiction (x=x+1 has no solution) | fate-open (empty anchor type: drift with no destination) |
| Time | does not flow (equalities are timeless) | explicit variable (evolution clock K^m) |

The two grammars are complementary, not substitutes: conservation statements are written with the equals sign; fate statements are written with the anchor sign. Standard mathematics is in fact already working between the two — the limit notation lim x→a f(x) = b embeds the composition of "→" (fate) and "=" (reading off the value); the anchor sign promotes this composition to a single first-class connective, making "having or lacking a destination" a question of type eligibility rather than a notational convention.

### 4.2 An Equation Reading of the History of the Rigorization of the Calculus

Anchor numbers [2], §4.2, reads the two-hundred-year rigorization history of the calculus as the first anchor collapse. The anchor equations give that history a grammatical reading: Newton's fluxions wrote instantaneous relations with the equals sign, and the legitimacy of fate was called into question (Berkeley's "ghosts of departed quantities"); the ε-δ language of Cauchy-Weierstrass translated fate back into the grammar of the equals sign (the ε-δ definition of limits), at the cost of an exponentially rising writing cost for fate statements; the completeness of the reals (Dedekind-Cantor [5][6]) made fate statements decidable equations again. The anchor equations are the terminal form of this history at the grammar layer: fate no longer needs to be translated back into the equals sign — it has its own connective, calculus, and engine.

### 4.3 Positioning within Constructive Mathematics

The anchor equations are the notation-calculus layer of anchor numbers [2]: anchor numbers complete the "ontological completion of moving numbers"; the anchor equations complete "the equation-writing system for that ontology". Analogy: group theory is to group notation — axioms give the structure; notation gives the calculus. By the completion standard [3] (E5: absorption means replacement), this construction does not establish a new genealogy row.

## §5 Academic Comparisons

| Comparison system | Isomorphic aspect | Differentiating aspect | Verdict |
|---|---|---|---|
| Asymptotic notation ~ [12] | pointwise coincidence with the completion type (Theorem 2.11) | ~ is a predicate, the anchor sign is a type with a functionality certificate; the anchor sign has the empty anchor type and operations on the type lattice | nearest precedent; the anchor sign is its syntactic upgrade |
| Topological convergence → | the convergence semantics is adopted verbatim in the metric type / completion type | → has no functionality certificate, no type eligibility, and no right-hand slot for the empty anchor | absorbed as an instance |
| Banach contraction [9] | the entire instance basis of the metric type of the anchor sign | the Banach theorem states existence and does not provide an equation-writing form for destination | theorem layer vs. grammar layer |
| Tarski-Knaster [10][11] | the instance basis of the lattice-order type of the anchor sign | a fixed-point existence theorem, with no equation form for order convergence | theorem layer vs. grammar layer |
| Semigroup theory / operator semigroups [13] | the flow semigroup definition adopts the standard form directly | classical theory characterizes generators (Hille–Yosida); this paper characterizes the grammatical status of the evolution laws and the clock | instrumental relation, honest borrowing |
| Bishop constructivism [7] | completion = explicit construction steps (an extension of the dialogue piece of anchor numbers [2] §5.3) | Bishop rejects the completed reading; the anchor sign does not presuppose completion, and the empty anchor type is precisely the legitimate form of the "uncompleted" | dialogue continued |
| Domain theory, the Kleene fixed point [14] | the ω-continuous special case of the lattice-order type (iterated sup = least fixed point) | this paper does not assume ω-continuity (honest boundary of 2.8); domain theory is the special-case layer | special-case relation |

Verdict of no peer precedent: at the connective level (~, →, categorical arrows), none promoted destination to a type with a functionality certificate; at the engine level (the substitution vs. evolution contrast) there is no prior formulation; "fate-open = legitimate right-hand slot of the empty anchor type" has no precedent.

## §6 Open Problems

1. **A complete calculus of the anchor sign**: the anchor-engine counterpart of the term rewriting system of the equality engine (substitution / transitivity / symmetry) — an anchor-sign version of the term rewriting rule set and its confluence;
2. **Parametrization of clock functions**: a classification of the canonical forms of the rate function c; the construction piece of the exp(−λt) instance and the boundary of generator characterization (honest boundary of §3.4);
3. **The ω-continuous special case of the lattice-order type**: the anchor-sign version of "under the assumption that f preserves countable suprema, the iterated supremum = the least fixed point" (the form of the Kleene theorem [14]);
4. **The order version of the clock and collectivity**: candidates for the quantitative form of "tightening at every step" of evolution in the order (chain-height step count);
5. **A generative grammar of the anchor equations**: what counts as a legitimate anchor equation (a BNF-level grammar definition) — whether the left component of the anchor sign may be a combination of equations, and union / intersection operations on right-component types.

---

## References

[1] Qin Chao. 密度数学（一）：数的密度聚类理论——静力学核心. Zenodo, 2026. doi:10.5281/zenodo.22773691. (Density Mathematics I: The Density-Clustering Theory of Numbers — The Static Core.)
[2] Qin Chao. 锚数：完备动数——数的动力学本体的锚定构造. Zenodo, 2026. doi:10.5281/zenodo.22866459. (Anchor Numbers: The Completed Dynamic Number — An Anchored Construction of the Dynamic Ontology of Numbers.)
[3] Qin Chao. 构造数学认证标准 v1.3. Zenodo, 2026. doi:10.5281/zenodo.22874646. (Certification Standard for Constructive Mathematics v1.3.)
[4] Qin Chao. 静的显化理论：自发动力学的公理化构造. Zenodo, 2026. doi:10.5281/zenodo.22785052. (The Theory of the Manifestation of the Static: An Axiomatic Construction of Spontaneous Dynamics.)
[5] Cantor, G. Ueber die Ausdehnung eines Satzes aus der Theorie der trigonometrischen Reihen. Mathematische Annalen 5, 1872, 123-132. doi:10.1007/BF01446327.
[6] Dedekind, R. Stetigkeit und irrationale Zahlen. Braunschweig: Friedrich Vieweg und Sohn, 1872. (First edition; verifiable: Open Library OL20470389M.)
[7] Bishop, E., Bridges, D. Constructive Analysis. Grundlehren der mathematischen Wissenschaften 279. Springer, 1985. doi:10.1007/978-3-642-61667-9.
[8] 创始人种子一：锚数式提案（2026-09-21，创始人原话，原话全文见附录 B.1）。 (Founder Seed One: The Anchor Equations Proposal (2026-09-21, verbatim words of the founder; full verbatim text in Appendix B.1).)
[9] Banach, S. Sur les opérations dans les ensembles abstraits et leur application aux équations intégrales. Fundamenta Mathematicae 3, 1922. doi:10.4064/fm-3-1-133-181.
[10] Tarski, A. A lattice-theoretical fixpoint theorem and its applications. Pacific Journal of Mathematics 5(2), 1955, 285-309.
[11] Knaster, B. Un théorème sur les fonctions d'ensembles. Annales de la Société Polonaise de Mathématique 6, 1928, 133-134. (Original volume scan verifiable: cybra.lodz.pl.)
[12] de Bruijn, N.G. Asymptotic Methods in Analysis. New York: Dover, 1981 (unabridged republication of the 3rd edition). ISBN 978-0-486-64221-5.
[13] Pazy, A. Semigroups of Linear Operators and Applications to Partial Differential Equations. Applied Mathematical Sciences 44. Springer, 1983. doi:10.1007/978-1-4612-5561-1.
[14] Davey, B.A., Priestley, H.A. Introduction to Lattices and Order, 2nd ed. Cambridge University Press, 2002. ISBN 978-0-521-78451-1. doi:10.1017/CBO9780511809088.

## Appendix A: Lean Formalization Inventory

This repository's `AnchorLayer.lean` (Mathlib foundation; `lake build` passes the whole project, 8717 jobs):

- Anchor-sign calculus section: AnchorType structure / anchor-sign notation (scoped notation) / the four rules (anchored_dest/anchored_mono/anchored_agree/empty_not_anchored — **zero axiom dependence throughout**) / metricType/metric_anchored/completionType/completion_anchored/plus1_not_anchored/orderType/order_anchored_intro (zero axioms) / tarski_lfp_anchored/completion_sub_iff_dist;
- Evolution engine section: evolve_step_le/evolve_iterate_le/evolve_edist_mono/evolve_edist_bound/evolve_edist_pair (carrier generalized to EMetricSpace) / composition rules (evolve_comp_contracting/evolve_clock_add/evolve_comp_pair/comp_metric_anchored/evolve_comp_assoc/evolve_comp_bound) / FlowSemigroup/flow_iterate_eq/flow_edist_mono/flow_edist_bound/flow_edist_pair/flow_point_bound/flow_rate_submul/flow_clock_mono;
- Order-type evolution section: order_iterate_step_le/order_iterate_antitone/order_iterate_mono_le/order_iterate_eq_fixed.

Zero sorry (self-contained proofs; no axiom, no sorry, no native_decide); #print axioms on the main theorems gives only the three standard axioms (propext/Classical.choice/Quot.sound) or fewer. The axiom audit and reproduction instructions accompany the repository (anchor-equations).

## Appendix B: Statement of Observational Origins

**B.1 (the anchor equations proposal, 2026-09-21, verbatim anchor [8])**: "Anchor equations can be non-conservation equations: the left side is the direction of numbers, the middle is the anchor sign (not an equals sign, nor a greater-than or less-than sign), and the right side is a description of an anchor dynamical type — supplementing the equalities that standard mathematics starts from various conservations; starting from the movement of the dynamic nature of numbers, it can be the anchor sign."
**B.2 (the evolution engine proposal, 2026-09-21, verbatim anchor [9] section)**: "Since the anchor equations are a representation of the dynamic ontology of numbers, then we should think about the evolution of the moving ontology. What I have in mind is that anchor numbers should not use the substitution of standard mathematics but evolution, introducing the time variable."
Note on the stratification of the observation chain: both seeds grew from inside the completion practice of anchor numbers [2] (first the family of anchor theorems, then the grammar proposal) — an instance, at the notation layer, of "observation precedes inference".

## Citation Verification Statement

All 14 references were verified against primary sources (2026-09-21; CrossRef official API / publisher official pages / MARC records of national-level libraries / page-by-page checking against scans of the original volumes), with two corrections on record: (1) Cantor 1872 — the DOI 10.1007/BF01445827 transmitted by search summaries was verified via CrossRef not to exist (a hallucinated DOI intercepted); the correct DOI is 10.1007/BF01446327 (Math. Ann. 5, 123-132). (2) Davey-Priestley, 2nd edition — the hardcover ISBN 0-521-78303-8 transmitted by search summaries was verified via BnF/Open Library to belong to a different book; the 2nd edition has only the paperback ISBN 978-0-521-78451-1. The circulating hardcover ISBN of Bishop-Bridges has an invalid check digit; the Springer DOI is cited instead. The original spelling Ueber (the wording of Springer's bibliographic record for Cantor) is retained.

## Method Note (AI Participation)

The axiom seeds and proposals of this research were put forward by the founder (Qin Chao) (verbatim anchors in Appendix B); the AI system of this framework (Vortex (Wo)) carried out the formal verification (Lean 4/Mathlib, zero sorry), the literature provenance search, and the writing of the paper. The human–machine division of labor is auditable: all machine proofs can be independently rechecked (Appendix A repository).
