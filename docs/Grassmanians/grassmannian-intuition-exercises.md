# Grassmannian Intuition: A Progressive Exercise Set

**Companion to:** The Signature Intuition exercises; Fulton, *Young Tableaux*
**Prerequisite:** Linear algebra (subspaces, bases, dimension); basic familiarity with projective space; geometric algebra fundamentals
**Goal:** Develop geometric intuition for Grassmannians, Schubert cells, and intersection theory — the mathematical substrate of ShaperOS capability resolution

---

## How to Use This Document

Same Predict → Compute → Reflect structure as the signature exercises. Grassmannian intuition is harder to build than signature intuition because Grassmannians are *spaces of subspaces* — you're reasoning about points whose "coordinates" are themselves geometric objects. The antidote is relentless concreteness: draw pictures, write down explicit matrices, count things by hand.

**Notation conventions:**
- Gr(k,n) = the Grassmannian of k-dimensional subspaces of ℝⁿ (or ℂⁿ)
- We use 1-indexed coordinates unless stated otherwise
- [n] = {1, 2, ..., n}
- A "k-plane" means a k-dimensional linear subspace (always through the origin)
- Column vectors in a k × n matrix represent a basis for a k-plane; the row-reduced echelon form is the canonical representative

---

## Stage 1: What Is a Grassmannian?

### Core Idea

A Grassmannian Gr(k,n) is a *space whose points are k-dimensional subspaces of an n-dimensional vector space*. This is strange: each "point" of Gr(k,n) is itself a geometric object (a k-plane through the origin in ℝⁿ).

The simplest analogy: the unit sphere S² is the space of directions in ℝ³. Each "point" of S² is a direction — a 1-dimensional object. The Grassmannian generalizes this: Gr(k,n) is the space of "k-dimensional directions."

### Exercise 1.1: Grassmannians You Already Know

**Predict, then verify:** Which familiar geometric spaces are Grassmannians in disguise?

(a) **Gr(1,2):** The space of 1-dimensional subspaces (lines through the origin) in ℝ². 

Every line through the origin in ℝ² is determined by its slope (or "vertical" for the y-axis). This is a single parameter — the angle θ ∈ [0, π) — with the endpoints identified. Gr(1,2) ≅ ℝP¹ ≅ S¹ (the circle). It's 1-dimensional.

**Dimension check:** dim Gr(k,n) = k(n−k). Here: 1·(2−1) = 1. ✓

(b) **Gr(1,3):** Lines through the origin in ℝ³.

Each line is determined by a direction vector, up to scaling. This is ℝP² — the real projective plane. Two parameters (e.g., two angles on the sphere, with antipodal identification).

**Dimension check:** 1·(3−1) = 2. ✓

(c) **Gr(1,n):** Lines through the origin in ℝⁿ.

This is ℝPⁿ⁻¹ — real projective (n−1)-space. The Grassmannian of lines is always a projective space. Dimension: 1·(n−1) = n−1. ✓

(d) **Gr(n−1, n):** Hyperplanes (codimension-1 subspaces) in ℝⁿ.

A hyperplane through the origin in ℝⁿ is determined by its normal direction (up to scaling). So Gr(n−1, n) ≅ ℝPⁿ⁻¹ too!

**Dimension check:** (n−1)·(n−(n−1)) = (n−1)·1 = n−1. ✓

**Key insight:** Gr(k,n) ≅ Gr(n−k, n). The space of k-planes is "the same" as the space of (n−k)-planes, via the orthogonal complement map V ↦ V⊥. This duality will reappear everywhere.

(e) **Gr(2,4):** 2-planes in ℝ⁴.

This is the first Grassmannian that isn't a projective space. Dimension: 2·(4−2) = 4. It's a compact, smooth 4-dimensional manifold. This is the Grassmannian that powers ShaperOS's basic capability examples (σ₁⁴ = 2 lives here).

### Exercise 1.2: Counting Dimensions

**Predict the dimension of each Grassmannian, then verify with k(n−k):**

| Grassmannian | Your prediction | k(n−k) |
|-------------|----------------|--------|
| Gr(2,5) | | 2·3 = 6 |
| Gr(3,6) | | 3·3 = 9 |
| Gr(2,7) | | 2·5 = 10 |
| Gr(4,8) | | 4·4 = 16 |
| Gr(1,100) | | 99 |
| Gr(50,100) | | 50·50 = 2500 |

**Intuition for the formula:** A k-plane in ℝⁿ is specified by choosing a k×n matrix of rank k (whose rows span the plane). That's kn entries, but the plane doesn't change if you apply an invertible k×k matrix to the rows (change of basis within the plane). So the dimension is kn − k² = k(n−k).

Alternatively: a k-plane V has a (n−k)-dimensional orthogonal complement V⊥. Moving V infinitesimally means mapping each of the k basis vectors of V to a vector in V⊥, giving k(n−k) degrees of freedom. This is the tangent space interpretation.

**Note the symmetry:** dim Gr(k,n) = dim Gr(n−k,n) = k(n−k). Maximum dimension at k = n/2: the "middle" Grassmannian has the most room.

### Exercise 1.3: Visualizing Gr(2,4)

This is the workhorse example. Every Schubert calculus exercise and every ShaperOS capability example in the existing codebase uses Gr(2,4). Build a thorough mental model.

**A point of Gr(2,4)** is a 2-plane through the origin in ℝ⁴. You can represent it as the row space of a 2×4 matrix of rank 2:

```
V = rowspan [a₁ a₂ a₃ a₄]
             [b₁ b₂ b₃ b₄]
```

Row-reduce to echelon form. The two pivots are in some columns i < j. The possible pivot positions are the 2-element subsets of {1,2,3,4}: there are C(4,2) = 6 of them.

**Example pivot positions and what they mean geometrically:**

Pivots in columns {1,2}:
```
[1  0  *  *]
[0  1  *  *]
```
The plane contains e₁ and e₂, plus perturbations in the e₃, e₄ directions. The four *'s are the local coordinates on this patch of Gr(2,4).

Pivots in columns {1,3}:
```
[1  *  0  *]
[0  0  1  *]
```
The plane contains e₁ and e₃, plus perturbations. Again 4 free parameters.

Pivots in columns {3,4}:
```
[0  0  1  0]
[0  0  0  1]
```
Wait — this is only true if the first two columns are zero. More generally:
```
[*  *  1  0]
[*  *  0  1]
```
The plane contains e₃ and e₄, plus perturbations.

**Exercise:** Write down all 6 echelon forms for Gr(2,4) (one for each pivot pair). For each, count the number of free parameters. Verify each has exactly 4 = dim Gr(2,4) free parameters.

**Key insight:** These 6 open sets cover Gr(2,4) like an atlas of charts. Each chart looks like ℝ⁴ (or actually like a 2×2 matrix — 4 entries). The Grassmannian is the space you get by gluing these 6 copies of ℝ⁴ together along their overlaps.

### Exercise 1.4: Gr(k,n) Over Finite Fields

**Concrete counting exercise:** Over the finite field 𝔽_q (with q elements), how many points does Gr(k,n) have?

The answer is the **Gaussian binomial coefficient**:

```
|Gr(k,n)(𝔽_q)| = [n choose k]_q = (qⁿ − 1)(qⁿ − q)···(qⁿ − q^(k−1)) / ((q^k − 1)(q^k − q)···(q^k − q^(k−1)))
```

**Compute for small cases:**

(a) |Gr(1,3)(𝔽₂)| = (2³ − 1)/(2¹ − 1) = 7/1 = 7.

These are the 7 lines through the origin in 𝔽₂³ = {0,1}³. List them: a line is a nonzero vector up to scaling, but over 𝔽₂ the only scalar is 1, so each line is just a nonzero vector. There are 2³ − 1 = 7 nonzero vectors, each forming its own line. ✓

(b) |Gr(2,4)(𝔽₂)| = (2⁴−1)(2⁴−2)/((2²−1)(2²−2)) = 15·14/(3·2) = 210/6 = 35.

There are 35 two-dimensional subspaces of 𝔽₂⁴. Each is a set of 4 vectors (including 0), and contains 3 nonzero vectors. (Check: 35 planes × 3 nonzero vectors each = 105, and each nonzero vector lies in some number of planes. There are 15 nonzero vectors, so each lies in 105/15 = 7 planes. This is [3 choose 1]₂ = 7.)

**Why this matters:** The Gaussian binomial [n choose k]_q approaches the ordinary binomial C(n,k) as q → 1 (in a regularized sense). The "number of points" of a Grassmannian over 𝔽_q is a q-analog of the number of Schubert cells. This connection between finite geometry and topology is one of the deep themes underlying Schubert calculus.

---

## Stage 2: Plücker Coordinates

### Motivation

A point of Gr(k,n) is a k-plane, which is a complicated object. The Plücker embedding turns it into a point in projective space — something much simpler. The price: the projective space is bigger (dimension C(n,k) − 1 instead of k(n−k)), and not every point of the projective space corresponds to a k-plane. The Plücker relations cut out which points do.

This is exactly the Plücker embedding in the `amari-enumerative` corrections — fixing the map from Schubert classes to multivectors in Cl(n,0,0).

### Exercise 2.1: Plücker Coordinates for Gr(2,4)

A 2-plane V in ℝ⁴ is spanned by two vectors v₁, v₂. The **Plücker coordinates** are the 2×2 minors of the 2×4 matrix [v₁; v₂]:

```
p_{ij} = det [v₁ᵢ  v₁ⱼ]  for 1 ≤ i < j ≤ 4
             [v₂ᵢ  v₂ⱼ]
```

There are C(4,2) = 6 Plücker coordinates: p₁₂, p₁₃, p₁₄, p₂₃, p₂₄, p₃₄.

These are defined up to an overall scalar (changing the basis of V scales all pᵢⱼ by the determinant of the basis change), so the Plücker map is:

Gr(2,4) → ℝP⁵ : V ↦ [p₁₂ : p₁₃ : p₁₄ : p₂₃ : p₂₄ : p₃₄]

**Compute the Plücker coordinates of these specific 2-planes:**

(a) V = span(e₁, e₂):
```
Matrix: [1 0 0 0]
        [0 1 0 0]

p₁₂ = det[1 0; 0 1] = 1
p₁₃ = det[1 0; 0 0] = 0
p₁₄ = det[1 0; 0 0] = 0
p₂₃ = det[0 0; 1 0] = 0
p₂₄ = det[0 0; 1 0] = 0
p₃₄ = det[0 0; 0 0] = 0

Plücker: [1 : 0 : 0 : 0 : 0 : 0]
```

This is a coordinate 2-plane — only one Plücker coordinate is nonzero.

(b) V = span(e₁ + e₃, e₂ + e₄):
```
Matrix: [1 0 1 0]
        [0 1 0 1]

p₁₂ = det[1 0; 0 1] = 1
p₁₃ = det[1 1; 0 0] = 0
p₁₄ = det[1 0; 0 1] = 1
p₂₃ = det[0 1; 1 0] = −1
p₂₄ = det[0 0; 1 1] = 0
p₃₄ = det[1 0; 0 1] = 1

Plücker: [1 : 0 : 1 : −1 : 0 : 1]
```

Multiple nonzero coordinates — this is a "generic" 2-plane.

(c) **Your turn:** Compute Plücker coordinates for V = span(e₁ + e₂, e₃ + e₄).

(d) **Your turn:** Compute for V = span(e₁ + 2e₂ + 3e₃, e₂ + e₃ + e₄).

### Exercise 2.2: The Plücker Relation

Not every point of ℝP⁵ is a Plücker image. The constraint is the **Plücker relation**:

```
p₁₂p₃₄ − p₁₃p₂₄ + p₁₄p₂₃ = 0
```

**Verify** for each of your computed examples above. For (b): 1·1 − 0·0 + 1·(−1) = 1 − 0 − 1 = 0. ✓

**Check a non-Plücker point:** Is [1 : 1 : 1 : 1 : 1 : 1] the Plücker coordinate of some 2-plane?

1·1 − 1·1 + 1·1 = 1 − 1 + 1 = 1 ≠ 0. **No.** This point of ℝP⁵ doesn't correspond to any 2-plane in ℝ⁴.

**Geometric meaning:** The Plücker relation says that the 6 maximal minors of a 2×4 matrix aren't independent — they satisfy an algebraic relation. The Grassmannian Gr(2,4) is a quadric hypersurface in ℝP⁵ (a 4-dimensional variety in 5-dimensional projective space).

**General pattern:** For Gr(k,n), the Plücker embedding goes to ℝP^(C(n,k)−1), and the Plücker relations are quadratic equations that cut out the Grassmannian as a subvariety. For Gr(2,n) there's a single family of relations; for larger k, the relations are more numerous.

### Exercise 2.3: Plücker Coordinates as Blades

**Connection to geometric algebra:** The Plücker coordinates of a 2-plane V = span(v₁, v₂) are exactly the coefficients of the 2-blade v₁ ∧ v₂ in Cl(n,0,0):

```
v₁ ∧ v₂ = Σ_{i<j} p_{ij} eᵢⱼ
```

**Verify:** For V = span(e₁ + e₃, e₂ + e₄) from Exercise 2.1(b):

```
(e₁ + e₃) ∧ (e₂ + e₄) = e₁∧e₂ + e₁∧e₄ + e₃∧e₂ + e₃∧e₄
                        = e₁₂ + e₁₄ − e₂₃ + e₃₄
```

Coefficients: p₁₂ = 1, p₁₃ = 0, p₁₄ = 1, p₂₃ = −1, p₂₄ = 0, p₃₄ = 1. Matches! ✓

**The Plücker relation is the blade condition:** A general bivector B = Σ_{i<j} b_{ij} eᵢⱼ is a **blade** (decomposable as v₁ ∧ v₂) if and only if B ∧ B = 0. For grade 2 in 4D, this reduces to exactly the Plücker relation.

**Compute:** B ∧ B for B = b₁₂e₁₂ + b₁₃e₁₃ + b₁₄e₁₄ + b₂₃e₂₃ + b₂₄e₂₄ + b₃₄e₃₄.

Since eᵢⱼ ∧ eᵢⱼ = 0, the only surviving terms are eᵢⱼ ∧ eₖₗ where {i,j} ∩ {k,ℓ} = ∅:

```
B ∧ B = 2(b₁₂b₃₄ − b₁₃b₂₄ + b₁₄b₂₃) e₁₂₃₄
```

Setting this to zero gives b₁₂b₃₄ − b₁₃b₂₄ + b₁₄b₂₃ = 0 — the Plücker relation. ✓

**Key insight:** In the GA framework, Gr(k,n) is the space of unit (normalized) k-blades in Cl(n,0,0), up to scaling. The Plücker embedding is "write down the blade's coefficients." The Plücker relations are "the blade is decomposable." This is why `amari-enumerative` uses Cl(n,0,0): blades *are* Plücker representatives.

### Exercise 2.4: Coordinate Patches via Plücker

In Exercise 1.3, we saw 6 coordinate charts for Gr(2,4). Each chart has a nonzero pivot minor.

**Connection:** The chart with pivots {i,j} is the open set where p_{ij} ≠ 0. On this chart, we can normalize p_{ij} = 1 and the remaining Plücker coordinates (subject to the Plücker relation) give 4 free parameters.

**Exercise:** On the chart p₁₂ ≠ 0, set p₁₂ = 1. The Plücker relation becomes:

```
p₃₄ − p₁₃p₂₄ + p₁₄p₂₃ = 0
```

So p₃₄ is determined by p₁₃, p₁₄, p₂₃, p₂₄. These 4 free coordinates are the local coordinates on this patch. They match the 4 free entries in the echelon form:

```
[1  0  −p₂₃  −p₂₄]
[0  1   p₁₃   p₁₄]
```

**Verify:** Compute the Plücker coordinates of this matrix and check they match.

```
p₁₂ = 1·1 − 0·0 = 1  ✓
p₁₃ = 1·p₁₃ − 0·(−p₂₃) = p₁₃  ✓
p₁₄ = 1·p₁₄ − 0·(−p₂₄) = p₁₄  ✓
p₂₃ = 0·p₁₃ − 1·(−p₂₃) = p₂₃  ✓
p₂₄ = 0·p₁₄ − 1·(−p₂₄) = p₂₄  ✓
p₃₄ = (−p₂₃)·p₁₄ − (−p₂₄)·p₁₃ = p₁₃p₂₄ − p₁₄p₂₃  ✓ (Plücker relation)
```

### Exercise 2.5: When Two Planes Are "Close"

**Geometric intuition builder:** In Gr(2,4), when are two 2-planes "nearby"?

Take V₀ = span(e₁, e₂) with Plücker [1:0:0:0:0:0]. Consider V_ε = span(e₁ + εe₃, e₂ + εe₄) for small ε.

**Compute Plücker coordinates of V_ε:**

```
p₁₂ = 1, p₁₃ = ε, p₁₄ = 0, p₂₃ = 0, p₂₄ = ε, p₃₄ = ε²
```

As ε → 0, V_ε → V₀. The "first-order" deformation is captured by p₁₃ and p₂₄ (both order ε), while p₃₄ = ε² is second-order.

**Tangent space interpretation:** The tangent space T_{V₀} Gr(2,4) consists of the first-order deformations. These are parameterized by 2×2 matrices (the non-pivot entries in the echelon form), which is Hom(V₀, V₀⊥) — linear maps from the plane to its complement. This is the origin of the dimension formula: dim Hom(V₀, V₀⊥) = k · (n−k).

**Exercise:** Compute the Plücker coordinates of span(e₁ + εe₃ + δe₄, e₂ − δe₃ + εe₄) and identify the first-order and second-order terms. How many independent first-order parameters are there?

---

## Stage 3: Schubert Cells

### Motivation

Schubert cells decompose the Grassmannian into pieces, each isomorphic to an affine space ℝᵈ. They're the building blocks for intersection theory, and understanding them concretely is essential for understanding what ShaperOS's capability intersection actually computes.

### Exercise 3.1: The Complete Flag

A **complete flag** in ℝ⁴ is a chain of subspaces:

F₁ ⊂ F₂ ⊂ F₃ ⊂ ℝ⁴

with dim Fᵢ = i. The **standard flag** is:

```
F₁ = span(e₁)
F₂ = span(e₁, e₂)
F₃ = span(e₁, e₂, e₃)
```

The Schubert cells of Gr(k,n) are defined relative to a chosen flag.

### Exercise 3.2: Schubert Cells of Gr(2,4)

Given the standard flag, a 2-plane V ∈ Gr(2,4) has a **position** relative to the flag, recorded by the dimensions:

```
dim(V ∩ F₁), dim(V ∩ F₂), dim(V ∩ F₃)
```

These dimensions are weakly increasing and satisfy 0 ≤ dim(V ∩ Fⱼ) ≤ min(2, j).

**Exercise:** Compute these dimensions for each of the following 2-planes and classify them:

(a) V = span(e₁, e₂):
```
V ∩ F₁ = span(e₁), dim = 1
V ∩ F₂ = span(e₁, e₂), dim = 2
V ∩ F₃ = span(e₁, e₂), dim = 2
```
Sequence: (1, 2, 2).

(b) V = span(e₁, e₃):
```
V ∩ F₁ = span(e₁), dim = 1
V ∩ F₂ = span(e₁), dim = 1
V ∩ F₃ = span(e₁, e₃), dim = 2
```
Sequence: (1, 1, 2).

(c) V = span(e₂, e₃):
```
V ∩ F₁ = {0}, dim = 0
V ∩ F₂ = span(e₂), dim = 1
V ∩ F₃ = span(e₂, e₃), dim = 2
```
Sequence: (0, 1, 2).

(d) V = span(e₁, e₄):
```
V ∩ F₁ = span(e₁), dim = 1
V ∩ F₂ = span(e₁), dim = 1
V ∩ F₃ = span(e₁), dim = 1
```
Sequence: (1, 1, 1).

(e) V = span(e₂, e₄):
```
V ∩ F₁ = {0}, dim = 0
V ∩ F₂ = span(e₂), dim = 1
V ∩ F₃ = span(e₂), dim = 1
```
Sequence: (0, 1, 1).

(f) V = span(e₃, e₄):
```
V ∩ F₁ = {0}, dim = 0
V ∩ F₂ = {0}, dim = 0
V ∩ F₃ = span(e₃), dim = 1
```
Sequence: (0, 0, 1).

**These are the 6 Schubert cells of Gr(2,4).** Each sequence of dimensions corresponds to a unique cell.

### Exercise 3.3: Partitions from Position Sequences

The position sequence is usually encoded as a **partition** λ. The translation: for Gr(k,n), the Schubert cell indexed by partition λ = (λ₁ ≥ λ₂ ≥ ⋯ ≥ λₖ ≥ 0) with λ₁ ≤ n−k consists of 2-planes V with:

```
dim(V ∩ F_{n−k+i−λᵢ}) ≥ i   for i = 1, ..., k
```

For Gr(2,4), k=2, n−k=2. The condition is:
```
dim(V ∩ F_{2+i−λᵢ}) ≥ i   for i = 1, 2
```

i.e., dim(V ∩ F_{3−λ₁}) ≥ 1 and dim(V ∩ F_{4−λ₂}) ≥ 2.

**Exercise:** Match each partition to the corresponding coordinate plane from Exercise 3.2.

| Partition λ | Condition | Coordinate plane | Position sequence |
|------------|-----------|-----------------|-------------------|
| (0,0) = ∅ | dim(V∩F₃) ≥ 1, dim(V∩F₄) ≥ 2 | ? | ? |
| (1,0) = □ | dim(V∩F₂) ≥ 1, dim(V∩F₄) ≥ 2 | ? | ? |
| (1,1) = □□ | dim(V∩F₂) ≥ 1, dim(V∩F₃) ≥ 2 | ? | ? |
| (2,0) = □□ | dim(V∩F₁) ≥ 1, dim(V∩F₄) ≥ 2 | ? | ? |
| (2,1) = □□□ | dim(V∩F₁) ≥ 1, dim(V∩F₃) ≥ 2 | ? | ? |
| (2,2) = □□□□ | dim(V∩F₁) ≥ 1, dim(V∩F₂) ≥ 2 | ? | ? |

Work through each: the partition (0,0) imposes the weakest conditions (any plane works); (2,2) imposes the strongest (the plane must contain F₂ = span(e₁,e₂)).

**Answers:**

| Partition | Codimension | Coordinate plane | Position sequence |
|-----------|-------------|-----------------|-------------------|
| ∅ | 0 | span(e₃,e₄) is a representative of the *open* cell | (0,0,1) |
| (1) | 1 | span(e₂,e₄) | (0,1,1) |
| (1,1) | 2 | span(e₂,e₃) | (0,1,2) |
| (2) | 2 | span(e₁,e₄) | (1,1,1) |
| (2,1) | 3 | span(e₁,e₃) | (1,1,2) |
| (2,2) | 4 | span(e₁,e₂) | (1,2,2) |

**Critical observation:** The codimension of the Schubert cell = |λ| = sum of the partition entries. This is why ShaperOS tracks codimension — it measures "how constrained" a capability is.

### Exercise 3.4: Cell Dimensions

Each Schubert cell σ°_λ (the open cell, not the closure) is isomorphic to ℝᵈ where d = dim Gr(k,n) − |λ| = k(n−k) − |λ|.

**Verify for Gr(2,4):**

| Cell | |λ| | Cell dimension | Cell ≅ |
|------|-----|----------------|--------|
| σ°_∅ | 0 | 4 | ℝ⁴ |
| σ°₁ | 1 | 3 | ℝ³ |
| σ°_{1,1} | 2 | 2 | ℝ² |
| σ°₂ | 2 | 2 | ℝ² |
| σ°_{2,1} | 3 | 1 | ℝ¹ |
| σ°_{2,2} | 4 | 0 | ℝ⁰ (a point) |

**Count the total:** The cells partition Gr(2,4) into disjoint pieces. Check:
- Number of cells: 6 (one per partition fitting in a 2×2 box)
- Euler characteristic: 1 + 1 + 1 + 1 + 1 + 1 = 6 (each ℝᵈ contributes (−1)ᵈ to Euler characteristic... actually that gives χ = 1−1+1+1−1+1 = 2? No.)

Actually, the Euler characteristic computed from the cell decomposition: χ = number of even-dimensional cells − number of odd-dimensional cells = (cells of dim 0, 2, 4) − (cells of dim 1, 3).

Even-dimensional: σ°_{2,2} (dim 0), σ°_{1,1} (dim 2), σ°₂ (dim 2), σ°_∅ (dim 4) → 4 cells.
Odd-dimensional: σ°_{2,1} (dim 1), σ°₁ (dim 3) → 2 cells.

χ = 4 − 2 ... hmm. Actually for CW complexes, χ = Σ (−1)^dim · (number of cells of that dimension):
= 1·(−1)⁰ + 0·(−1)¹ + 2·(−1)² + 1·(−1)³ + 1·(−1)⁴
= 1 + 0 + 2 − 1 + 1 = 3?

Wait, let me recount. Cells by dimension:
- dim 0: {σ°_{2,2}} — 1 cell
- dim 1: {σ°_{2,1}} — 1 cell
- dim 2: {σ°_{1,1}, σ°₂} — 2 cells
- dim 3: {σ°₁} — 1 cell
- dim 4: {σ°_∅} — 1 cell

χ = 1 − 1 + 2 − 1 + 1 = 2.

And |Gr(2,4)(𝔽₁)| = C(4,2) = 6 ... but χ = C(4,2) should hold for complex Grassmannians. Over ℝ, χ can differ.

**For the complex Grassmannian** (which is what Schubert calculus uses): dim_ℝ of each cell doubles (complex cells have even real dimension), so all cells contribute +1 to χ, giving χ = number of cells = C(n,k) = 6. This is consistent: |Gr(2,4)(𝔽₁)| = 6 matches C(4,2) = 6.

**Key insight:** Over ℂ, every Schubert cell has even real dimension, so the Euler characteristic equals the number of cells equals C(n,k). This is why the finite field count |Gr(k,n)(𝔽_q)| at q=1 gives the Euler characteristic.

### Exercise 3.5: Schubert Varieties (Closures)

The **Schubert variety** σ_λ is the closure of the Schubert cell σ°_λ. It contains all cells σ°_μ with μ ⊇ λ (μ dominates λ, meaning μᵢ ≥ λᵢ for all i).

**Exercise:** Draw the containment (Hasse diagram) for Schubert varieties in Gr(2,4).

The dominance partial order on partitions fitting in a 2×2 box:

```
        (2,2)
       /     \
    (2,1)     
    /    \     
  (2)   (1,1)
    \    /
     (1)
      |
     (∅)
```

Wait, let me be more careful. μ ⊇ λ means μ₁ ≥ λ₁ AND μ₂ ≥ λ₂.

- (2,2) ⊇ everything
- (2,1) ⊇ (2,0), (1,1), (1,0), (0,0)
- (2,0) ⊇ (1,0), (0,0)
- (1,1) ⊇ (1,0), (0,0)
- (1,0) ⊇ (0,0)
- (0,0) ⊇ (0,0)

Hasse diagram (covering relations only):

```
        (2,2)
       /     \
    (2,1)     |
    /    \    |
  (2,0)  (1,1)
    \    /
     (1,0)
       |
      (∅)
```

So σ_{(2,2)} = {span(e₁,e₂)} (just the top cell, a single point).
σ_{(2,1)} = σ°_{(2,1)} ∪ σ°_{(2,2)} = a 1-dimensional variety (isomorphic to ℝP¹).
σ_{(1)} = σ°_{(1)} ∪ σ°_{(2)} ∪ σ°_{(1,1)} ∪ σ°_{(2,1)} ∪ σ°_{(2,2)} = a 3-dimensional variety.
σ_∅ = Gr(2,4) (the whole Grassmannian).

**Exercise:** Verify that σ_{(1)} in Gr(2,4) is the set of all 2-planes V with dim(V ∩ F₂) ≥ 1 — that is, all 2-planes that have nontrivial intersection with the fixed 2-plane F₂ = span(e₁,e₂). This is a codimension-1 subvariety.

### Exercise 3.6: Young Diagrams

Draw the Young diagram for each partition. A partition λ = (λ₁, λ₂, ..., λₖ) is drawn as a left-justified array of boxes with λᵢ boxes in row i.

For Gr(2,4), partitions fit in a 2×2 box:

```
∅         (1)       (2)       (1,1)     (2,1)     (2,2)
          ┌─┐       ┌─┬─┐     ┌─┐       ┌─┬─┐     ┌─┬─┐
(empty)   │ │       │ │ │     ├─┤       ├─┤ │     ├─┤ │
          └─┘       └─┴─┘     │ │       │ │ │     │ │ │
                               └─┘       └─┴─┘     └─┴─┘
|λ|= 0     1         2         2          3          4
```

The **complement** of λ in the k×(n−k) box: rotate the Young diagram 180° and fit it into the remaining space. For Gr(2,4) (2×2 box):

- complement(∅) = (2,2)
- complement((1)) = (2,1)
- complement((2)) = (1,1)
- complement((1,1)) = (2)
- complement((2,1)) = (1)
- complement((2,2)) = ∅

**Note:** |λ| + |complement(λ)| = k(n−k) = 4 always. Complementation corresponds to Poincaré duality on the Grassmannian.

**For ShaperOS:** Two interfaces are "compatible" when their Schubert classes are complementary (their codimensions sum to the Grassmannian dimension). This is the type-checking rule for operadic composition.

---

## Stage 4: Intersection Theory

### Motivation

This is where the Grassmannian becomes a *calculator*. The product of Schubert classes σ_λ · σ_μ decomposes into a sum of Schubert classes with integer coefficients (Littlewood-Richardson coefficients). When the codimensions add up to the Grassmannian dimension, the product is a multiple of the point class — and that multiple is an intersection number, counting geometric configurations.

### Exercise 4.1: The Fundamental Intersection σ₁⁴ = 2

**Setup:** In Gr(2,4), the Schubert class σ₁ (codimension 1) represents the condition "the 2-plane meets a fixed 2-plane nontrivially." We impose four such conditions, one for each of four 2-planes in general position.

**Geometric question:** How many 2-planes in ℝ⁴ simultaneously meet four given 2-planes nontrivially?

Since dim Gr(2,4) = 4 and codim σ₁ = 1, imposing four conditions gives total codimension 4 = dim, so we expect a finite answer.

**The answer is 2.** This is the content of σ₁⁴ = 2σ_{2,2}, where σ_{2,2} is the point class.

**Concrete verification:** Take four 2-planes in "general position" in ℝ⁴:

```
P₁ = span(e₁, e₂)
P₂ = span(e₃, e₄)
P₃ = span(e₁ + e₃, e₂ + e₄)
P₄ = span(e₁ + e₄, e₂ + e₃)
```

**Find all 2-planes V that meet each Pᵢ nontrivially** (dim(V ∩ Pᵢ) ≥ 1 for each i).

Let V = span(v, w) where v = a₁e₁ + a₂e₂ + a₃e₃ + a₄e₄ and w = b₁e₁ + b₂e₂ + b₃e₃ + b₄e₄.

V meets P₁ nontrivially iff some nonzero linear combination αv + βw lies in span(e₁,e₂), i.e., the e₃, e₄ components vanish: αa₃ + βb₃ = 0 and αa₄ + βb₄ = 0. This means the vectors (a₃, a₄) and (b₃, b₄) are proportional (or one is zero).

This gets complicated with four simultaneous conditions. The cleaner approach is via the Plücker coordinates.

**Plücker approach:** V ∈ σ₁(Pᵢ) iff p ∧ qᵢ = 0, where p is the Plücker representative of V and qᵢ is the Plücker representative of Pᵢ.

Actually, for 2-planes in 4D, V meets P nontrivially iff their Plücker representatives satisfy:

```
p₁₂q₃₄ − p₁₃q₂₄ + p₁₄q₂₃ + p₂₃q₁₄ − p₂₄q₁₃ + p₃₄q₁₂ = 0
```

This is the condition that the bivectors p and q are "incident" — they share a common vector.

**Exercise:** Compute the Plücker coordinates of P₁, P₂, P₃, P₄ above, set up the four incidence equations plus the Plücker relation, and solve the resulting system. You should find exactly 2 solutions (up to the projective equivalence).

This is algebraically involved but completely explicit — a good exercise in keeping Plücker arithmetic straight. (Hint: use the p₁₂ = 1 chart and reduce to a system in 4 unknowns with 5 equations.)

### Exercise 4.2: Littlewood-Richardson by Hand

The **LR coefficient** c^ν_{λμ} counts the number of ways to fill the skew Young diagram ν/λ with content μ such that:

1. Each row is weakly increasing left to right
2. Each column is strictly increasing top to bottom
3. The word obtained by reading right-to-left, top-to-bottom satisfies the **lattice word** (or ballot) condition: at every step, the number of i's seen so far is ≥ the number of (i+1)'s seen so far.

**Compute σ₁ · σ₁ in Gr(2,4):**

σ₁ · σ₁ = Σ_ν c^ν_{(1),(1)} σ_ν

The possible ν have |ν| = |(1)| + |(1)| = 2. Partitions of 2 fitting in a 2×2 box: (2) and (1,1).

**For ν = (2):** Skew shape (2)/(1) is a single box in position (1,2). Fill with content (1) — put a 1 in that box. Reading word: "1". Lattice condition: trivially satisfied. c^{(2)}_{(1),(1)} = 1.

**For ν = (1,1):** Skew shape (1,1)/(1) is a single box in position (2,1). Fill with content (1) — put a 1. Reading word: "1". Lattice condition: satisfied. c^{(1,1)}_{(1),(1)} = 1.

**Result:** σ₁² = σ₂ + σ_{1,1}.

**Now compute σ₁² · σ₁ = σ₁³:**

σ₁³ = (σ₂ + σ_{1,1}) · σ₁ = σ₂ · σ₁ + σ_{1,1} · σ₁

**σ₂ · σ₁:** Need c^ν_{(2),(1)} for |ν| = 3. Possible ν: (2,1).

Skew shape (2,1)/(2) is a single box at position (2,1). Fill with 1. Word "1". Lattice ✓. c = 1.

No other ν of weight 3 fits in a 2×2 box. So σ₂ · σ₁ = σ_{2,1}.

**σ_{1,1} · σ₁:** Need c^ν_{(1,1),(1)} for |ν| = 3. Again only (2,1) fits.

Skew shape (2,1)/(1,1) is a single box at position (1,2). Fill with 1. Word "1". Lattice ✓. c = 1.

So σ_{1,1} · σ₁ = σ_{2,1}.

**Result:** σ₁³ = 2σ_{2,1}.

**Finally, σ₁⁴ = σ₁³ · σ₁ = 2σ_{2,1} · σ₁:**

σ_{2,1} · σ₁: Need c^ν_{(2,1),(1)} for |ν| = 4. Only (2,2) fits.

Skew shape (2,2)/(2,1) is a single box at position (2,2). Fill with 1. Word "1". Lattice ✓. c = 1.

**Result:** σ₁⁴ = 2σ_{2,2}. Since σ_{2,2} is the point class, **the intersection number is 2.** ✓

### Exercise 4.3: A Larger Product

**Compute σ₂ · σ_{1,1} in Gr(2,4):**

Need c^ν_{(2),(1,1)} for |ν| = 2 + 2 = 4. Only (2,2) fits.

Skew shape (2,2)/(2): second row, two boxes in positions (2,1) and (2,2).

Fill with content (1,1): put "1" in both boxes.

Row condition: 1 ≤ 1 ✓ (weakly increasing).
Column condition: column 1 has only one entry, column 2 has only one entry ✓ (vacuously strict).
Lattice word: read right-to-left, top-to-bottom: "11". At each step, count of 1's ≥ count of 2's. After "1": count(1) = 1 ≥ 0 = count(2) ✓. After "11": count(1) = 2 ≥ 0 ✓.

But wait — content (1,1) means we use two 1's. There are no 2's. So the lattice condition is trivially satisfied.

c^{(2,2)}_{(2),(1,1)} = 1.

**Result:** σ₂ · σ_{1,1} = 1 · σ_{2,2}. The intersection number is **1**.

**Geometric meaning:** There is exactly 1 two-plane in ℝ⁴ that simultaneously:
- Contains a given line (σ₂ condition: meet a given 2-plane in a line, which for the special Schubert class σ₂ means "contain a fixed 1-plane")
- Lies in a given 3-plane (σ_{1,1} condition)

This is obvious geometrically: a 2-plane containing a fixed line and lying in a fixed 3-plane is uniquely determined.

### Exercise 4.4: Intersection Number Table

**Fill in the complete multiplication table for Gr(2,4).** You've already computed most products above. The table encodes how every pair of Schubert classes multiplies.

Since the point class σ_{2,2} satisfies σ_{2,2} · σ_λ = σ_λ if λ = ∅ (and 0 otherwise for nontrivial λ), and σ_∅ is the identity, you mostly need:

| · | σ₁ | σ₂ | σ_{1,1} | σ_{2,1} |
|---|----|----|---------|---------|
| σ₁ | σ₂ + σ_{1,1} | σ_{2,1} | σ_{2,1} | σ_{2,2} |
| σ₂ | σ_{2,1} | σ_{2,2} | σ_{2,2} | 0 |
| σ_{1,1} | σ_{2,1} | σ_{2,2} | 0 | 0 |
| σ_{2,1} | σ_{2,2} | 0 | 0 | 0 |

Wait — I should double-check σ₂ · σ₂ and σ_{1,1} · σ_{1,1}.

**σ₂ · σ₂:** Total codim = 4 = dim. Need c^{(2,2)}_{(2),(2)}.

Skew shape (2,2)/(2): two boxes in row 2. Fill with content (2) — meaning two 1's. Same as before (the content (2) means λ = (2), so we fill with one 1 and one 2? No. Content μ = (2) means μ₁ = 2, so we use two entries labeled "1". 

Hmm, I need to be more careful. Content μ means we use μ₁ copies of "1", μ₂ copies of "2", etc. For μ = (2): μ₁ = 2, so we use two 1's.

Row 2: [1, 1]. Weakly increasing ✓. No column issues (single row). Word "11". Lattice ✓.

c^{(2,2)}_{(2),(2)} = 1. So σ₂² = σ_{2,2}. **Intersection number: 1.**

**σ_{1,1} · σ_{1,1}:** Total codim = 4 = dim. Need c^{(2,2)}_{(1,1),(1,1)}.

Skew shape (2,2)/(1,1): two boxes at positions (1,2) and (2,2). Fill with content (1,1): one "1" and one "2".

The two boxes share column 2 (positions (1,2) and (2,2)). Column-strict means column 2 must be strictly increasing top-to-bottom: the entry at (1,2) < entry at (2,2).

So (1,2) gets 1 and (2,2) gets 2. That's the only filling.

Row condition: row 1 is [_, 1] ✓. Row 2 is [_, 2] ✓.
Word: right-to-left, top-to-bottom: "1, 2". After "1": count(1)=1 ≥ count(2)=0 ✓. After "1,2": count(1)=1 ≥ count(2)=1 ✓.

c = 1. So σ_{1,1}² = σ_{2,2}. **Intersection number: 1.**

Hmm, but the table says σ_{1,1} · σ_{1,1} = 0. Let me re-examine. Oh wait, for Gr(2,4), σ_{1,1} is codimension 2 and σ_{2,2} is the point class (codimension 4). σ_{1,1}² has codimension 4, so it should be a multiple of σ_{2,2}. My computation gives coefficient 1. But I recall that σ₂ · σ_{1,1} = σ_{2,2} and σ₁₁² should be... let me redo this.

Actually, I think I may have an error. Let me recheck σ_{1,1}²:

Skew shape (2,2)/(1,1) has boxes at (1,2) and (2,2) — the rightmost column. Wait: (2,2) is the partition with two rows of length 2. (1,1) has two rows of length 1. The skew diagram:

```
(2,2):    ┌─┬─┐     (1,1):   ┌─┐
          ├─┼─┤              ├─┤
          └─┴─┘              └─┘

Skew (2,2)/(1,1):    _  ┌─┐
                     _  ├─┤ 
                        └─┘
```

So the skew shape has 2 boxes: positions (1,2) and (2,2). Fill with content (1,1), meaning one "1" and one "2".

Column 2 has both boxes, strictly increasing requires top < bottom. Only filling: 1 on top, 2 on bottom.

Reading word (right-to-left, top-to-bottom): read row 1 right-to-left: "1". Then row 2 right-to-left: "2". Full word: "1, 2". At each prefix: after "1", #1's = 1 ≥ #2's = 0 ✓. After "1,2", #1's = 1 ≥ #2's = 1 ✓.

So c^{(2,2)}_{(1,1),(1,1)} = 1. σ_{1,1}² = σ_{2,2}.

Let me also verify: σ_{2} · σ_{1,1}.

Skew (2,2)/(2): row 2 is full (two boxes at (2,1) and (2,2)). Content (1,1): use one "1" and one "2".

Row must be weakly increasing: [1, 2] or [1, 1] or [2, 2]. But content has exactly one 1 and one 2, so [1, 2].

Column conditions: column 1 has only (2,1) with "1"; column 2 has only (2,2) with "2". No column violations (single entries per column).

Word: right-to-left top-to-bottom: row 1 is empty (all in ν\λ = row 2). Read row 2 right-to-left: "2, 1". After "2": #1's = 0 < #2's = 1. **Lattice violation!**

So c^{(2,2)}_{(2),(1,1)} = 0? But I computed 1 earlier!

Let me recheck. Earlier I used content μ = (1,1) meaning two copies of "1". That's the partition (1,1) interpreted as μ₁ = 1, μ₂ = 1 → one "1" and one "2". But wait, when I wrote "fill with content (1,1): put '1' in both boxes", I was treating the content as meaning two 1's. I conflated two conventions.

**Convention clarification:** Content μ means: the filling uses μ₁ entries labeled "1", μ₂ entries labeled "2", etc. So μ = (1,1) means one "1" and one "2". But μ = (2) means two "1"s.

Re-examining σ₂ · σ_{1,1}: we want c^ν_{(2),(1,1)}. Here λ = (2), μ = (1,1).

Skew (2,2)/(2): boxes at (2,1) and (2,2).
Content (1,1): one "1" and one "2".

**Filling [1,2] in row 2:** Word = "2,1" (right-to-left). After "2": #1=0 < #2=1. Lattice fail ✗.

**Filling [2,1]:** Not weakly increasing. Invalid.

So c^{(2,2)}_{(2),(1,1)} = 0, meaning σ₂ · σ_{1,1} = 0? But geometrically we argued it should be 1!

**The issue:** The LR rule computes c^ν_{λ,μ} but the Schubert product is σ_λ · σ_μ = Σ c^ν_{λ,μ} σ_ν. The coefficient c^{(2,2)}_{(2),(1,1)} counts fillings of shape (2,2)/(2) with content (1,1). I just showed it's 0.

But the geometric intersection σ₂ · σ_{1,1} should be σ_{2,2} (intersection number 1) by the classical result. What's wrong?

**Resolution:** I'm confusing two conventions. The LR coefficient c^ν_{λ,μ} as I defined it counts tableaux of skew shape ν/λ with content μ. But the Schubert multiplication rule is:

σ_λ · σ_μ = Σ_ν c^ν_{λ,μ} σ_ν

where c^ν_{λ,μ} counts LR tableaux of shape ν/λ with content **equal to μ**. Content equal to μ means the weight vector of the filling is μ.

For ν = (2,2), λ = (2), the skew shape is two boxes in row 2. Content = μ = (1,1) means: 1 box labeled "1" and 1 box labeled "2".

The only semistandard filling is [1,2] (weakly increasing across the row). Reading word right-to-left is "2,1". At the first step, we read "2" and check: number of 1's seen (0) ≥ number of 2's seen (1)? No. 0 < 1. **Lattice word condition fails.**

So c^{(2,2)}_{(2),(1,1)} = 0 by LR rule. This means σ₂ · σ_{1,1} has no σ_{2,2} term, hence **σ₂ · σ_{1,1} = 0** in the Schubert ring of Gr(2,4)!

**Wait — but the geometric argument!** The geometric argument said there's exactly 1 plane containing a line and lying in a hyperplane. Let me reconsider: σ₂ in Gr(2,4) means codimension 2, partition (2). The Schubert variety σ₂ (with respect to the standard flag) is the set of 2-planes V with dim(V ∩ F₁) ≥ 1, i.e., V contains the line span(e₁). The Schubert variety σ_{1,1} is the set of V with dim(V ∩ F₃) ≥ 2, i.e., V ⊂ F₃ = span(e₁,e₂,e₃).

σ₂ ∩ σ_{1,1} = {V : e₁ ∈ V, V ⊂ span(e₁,e₂,e₃)} = {planes through e₁ in span(e₁,e₂,e₃)}. These planes are span(e₁, ae₂ + be₃) for [a:b] ∈ ℝP¹. This is a **1-dimensional** family, not a point!

But codim(σ₂) + codim(σ_{1,1}) = 2 + 2 = 4 = dim Gr(2,4). So the intersection should be 0-dimensional (transverse) or empty. The 1-dimensional intersection means these two specific Schubert varieties (with respect to the same flag) are **not in general position**. The intersection number σ₂ · σ_{1,1} as a class is 0 because in the cohomology ring this product vanishes.

**But we should use different flags!** When we write σ₂ · σ_{1,1}, we mean the intersection of σ₂ defined by one flag and σ_{1,1} defined by a *different, general* flag. For two flags in general position, the intersection is transverse and the number of points equals the intersection number.

This actually reveals that σ₂ · σ_{1,1} = σ_{2,2}, not 0. The LR computation should give 1.

Let me recompute more carefully. The issue is in the reading order or the content convention.

**Alternative approach — use Pieri's rule instead:**

Pieri's formula: σ_p · σ_λ = Σ σ_μ, summing over all μ obtained from λ by adding p boxes, no two in the same column, such that μ is still a valid partition for Gr(k,n).

σ_{1,1} · σ₁ (using Pieri with p=1 and λ=(1,1)): add 1 box to (1,1), not creating two boxes in one column beyond the first added. We can get (2,1). ✓

Actually, the better Pieri formula for the product with σ_p (a single-row partition):

σ_p · σ_λ = Σ σ_μ where μ/λ is a horizontal strip of size p (no two boxes in the same column).

So σ₂ · σ_{1,1}: μ/λ = μ/(1,1) should be a horizontal strip of size 2. μ must fit in the 2×2 box. Starting from (1,1), we need to add 2 boxes with no two in the same column:

- Add one box to row 1 and one box to row 2: get (2,2). The two new boxes are in columns 2 and 2 — same column! Not a horizontal strip.

Hmm. Let me reconsider. A horizontal strip means no two new boxes in the same **column**. New boxes: position (1,2) and position (2,2) are both in column 2. So this is NOT a horizontal strip.

What about adding both boxes to row 1? From (1,1) → (3,1)? But 3 > n−k = 2, so (3,1) doesn't fit in the 2×2 box.

So there are **no valid μ**, and σ₂ · σ_{1,1} = 0 in Gr(2,4).

**This is actually correct!** Let me reconsider the geometry. σ₂ (for a general flag) represents 2-planes containing a general line ℓ. σ_{1,1} (for a different general flag) represents 2-planes contained in a general 3-plane H. For ℓ in general position with respect to H, ℓ is not contained in H (since a line in ℝ⁴ is 1D and a 3-plane is 3D, and a generic line meets a generic 3-plane in a point, not in a line). So a 2-plane containing ℓ can't lie entirely in H unless ℓ ⊂ H. For generic flags, ℓ ⊄ H, so the intersection **is empty**. σ₂ · σ_{1,1} = 0. ✓

**Corrected table:**

| · | σ₁ | σ₂ | σ_{1,1} | σ_{2,1} |
|---|----|----|---------|---------|
| σ₁ | σ₂ + σ_{1,1} | σ_{2,1} | σ_{2,1} | σ_{2,2} |
| σ₂ | σ_{2,1} | σ_{2,2} | 0 | 0 |
| σ_{1,1} | σ_{2,1} | 0 | σ_{2,2} | 0 |
| σ_{2,1} | σ_{2,2} | 0 | 0 | 0 |

**Key insight from this exercise:** Carefully distinguishing σ₂ from σ_{1,1} matters — they have the same codimension but different geometry. σ₂ ↔ "contains a line" while σ_{1,1} ↔ "lies in a hyperplane." Their product is zero because these conditions are generically incompatible. But σ₂² = σ_{2,2} (two "contains a line" conditions) and σ_{1,1}² = σ_{2,2} (two "lies in a hyperplane" conditions) both give 1.

**The LR tableau exercise caught a real geometric subtlety.** Getting confused and then resolving the confusion is exactly the point.

### Exercise 4.5: Interpreting ShaperOS Capabilities

**Recast the above in ShaperOS language:**

In Gr(2,4): a namespace is a 2-plane in 4D "capability space."

- σ₁ = "namespace has nontrivial overlap with a reference plane" (basic access condition)
- σ₂ = "namespace contains a fixed line" (strong condition: must include a specific capability)
- σ_{1,1} = "namespace lies inside a fixed 3-plane" (containment condition: restricted to a subspace)
- σ_{2,1} = "both: contains a line AND is restricted to a 3-plane" (very constrained)
- σ_{2,2} = "the namespace is completely determined" (unique configuration)

**σ₁⁴ = 2:** "Four basic access conditions, each imposed by a different reference, yield exactly 2 valid namespace configurations." This is the ShaperOS "two lines" theorem.

**σ₂ · σ_{1,1} = 0:** "A namespace that must include a specific capability AND be restricted to a subspace: generically impossible." The capability and the restriction are incompatible. ShaperOS should report `AccessResult::Denied`.

**σ₂² = 1:** "A namespace that must include two specific lines: exactly one such plane." If two line-capabilities are imposed, they determine the namespace uniquely (the plane spanned by those two lines).

**Exercise:** For Gr(2,5) (dimension 6), compute σ₁⁶ using the Pieri rule iteratively. The answer should be 5 — the number of lines meeting 6 general 3-planes in ℝ⁵. (This is the degree of the Grassmannian Gr(2,5) under the Plücker embedding.)

---

## Stage 5: Combinatorial Machinery

### Exercise 5.1: Hook-Length Formula

The number of standard Young tableaux of shape λ (relevant for counting dimensions of representations and for Schubert calculus) is given by the **hook-length formula**:

```
f^λ = n! / ∏_{(i,j) ∈ λ} hook(i,j)
```

where hook(i,j) = (number of boxes to the right of (i,j) in row i) + (number of boxes below (i,j) in column j) + 1.

**Compute for the partitions in Gr(2,4):**

(a) λ = (2,1): boxes at (1,1), (1,2), (2,1).

Hook lengths:
- (1,1): 2 right + 1 below + 1 = 3... wait: hook(1,1) = (number of boxes strictly right in row 1) + (number of boxes strictly below in column 1) + 1 = 1 + 1 + 1 = 3.
- (1,2): 0 + 0 + 1 = 1.
- (2,1): 0 + 0 + 1 = 1.

f^{(2,1)} = 3! / (3 · 1 · 1) = 6/3 = 2.

(b) λ = (2,2): boxes at (1,1), (1,2), (2,1), (2,2).

Hook lengths:
- (1,1): 1 + 1 + 1 = 3
- (1,2): 0 + 1 + 1 = 2
- (2,1): 1 + 0 + 1 = 2
- (2,2): 0 + 0 + 1 = 1

f^{(2,2)} = 4! / (3 · 2 · 2 · 1) = 24/12 = 2.

**Connection to Gr(k,n):** The degree of Gr(k,n) under the Plücker embedding (the number σ₁^{k(n-k)}) is related to the number of standard Young tableaux of rectangular shape k × (n-k):

```
deg Gr(k,n) = (k(n-k))! / ∏_{(i,j)} hook(i,j)
```

where the product is over the k × (n-k) rectangle.

**Verify for Gr(2,4):** Rectangle 2×2. Hook lengths: 3, 2, 2, 1 (same as λ = (2,2) above).

deg = 4!/(3·2·2·1) = 2. This is σ₁⁴ = 2. ✓

**Compute for Gr(2,5):** Rectangle 2×3. Boxes: (1,1), (1,2), (1,3), (2,1), (2,2), (2,3).

Hook lengths:
- (1,1): 2 + 1 + 1 = 4
- (1,2): 1 + 1 + 1 = 3
- (1,3): 0 + 1 + 1 = 2
- (2,1): 2 + 0 + 1 = 3
- (2,2): 1 + 0 + 1 = 2
- (2,3): 0 + 0 + 1 = 1

deg = 6! / (4·3·2·3·2·1) = 720/144 = 5. So σ₁⁶ = 5 in Gr(2,5). ✓

### Exercise 5.2: The Catalan Connection

**Compute deg Gr(2,n) for n = 3, 4, 5, 6, 7:**

All use 2 × (n-2) rectangles.

| n | Rectangle | deg = (2(n-2))! / ∏ hooks | Value |
|---|-----------|---------------------------|-------|
| 3 | 2×1 | 2!/(2·1) = 1 | 1 |
| 4 | 2×2 | 4!/(3·2·2·1) = 2 | 2 |
| 5 | 2×3 | 6!/(4·3·2·3·2·1) = 5 | 5 |
| 6 | 2×4 | 8!/(5·4·3·2·4·3·2·1) = 14 | 14 |
| 7 | 2×5 | 10!/(6·5·4·3·2·5·4·3·2·1) = 42 | 42 |

**Recognize the sequence:** 1, 2, 5, 14, 42 — these are the **Catalan numbers**!

deg Gr(2,n) = C_{n-2} = (1/(n-1)) · C(2(n-2), n-2).

**Key insight:** The degree of Gr(2,n) — equivalently, the number of lines meeting 2(n-2) general (n-2)-planes in ℙⁿ⁻¹ — is a Catalan number. This is one of the most elegant results in enumerative geometry, and it's computed by the hook-length formula for a 2-row rectangle.

### Exercise 5.3: Dual Grassmannian

**Verify the duality** Gr(k,n) ↔ Gr(n-k,n) at the level of intersection numbers.

The complement map sends λ ↦ λ^c where (λ^c)ᵢ = (n-k) - λ_{k+1-i}. This corresponds to σ_λ ↦ σ_{λ^c} under the isomorphism Gr(k,n) ≅ Gr(n-k,n).

**Check:** In Gr(2,4), the complement of (1) in the 2×2 box:
(λ^c)₁ = 2 - λ₂ = 2 - 0 = 2
(λ^c)₂ = 2 - λ₁ = 2 - 1 = 1

So σ₁ in Gr(2,4) maps to σ_{2,1} in Gr(2,4). This makes sense: σ₁ has codimension 1, σ_{2,1} has codimension 3, and 1 + 3 = 4 = dim Gr(2,4). They're Poincaré dual.

**Verify the intersection pairing:** σ_λ · σ_{λ^c} should be σ_{2,2} (the point class) with coefficient 1, and σ_λ · σ_μ = 0 when μ ≠ λ^c (for complementary codimension).

σ₁ · σ_{2,1}: from our table, this is σ_{2,2} with coefficient 1. ✓
σ₂ · σ_{1,1}: this is 0, which is consistent because (2)^c = (1,1)... wait, let me check: complement of (2) in 2×2: (λ^c)₁ = 2 - λ₂ = 2 - 0 = 2, (λ^c)₂ = 2 - λ₁ = 2 - 2 = 0. So (2)^c = (2,0) = (2). But that means σ₂ is self-complementary, and σ₂ · σ₂ = σ_{2,2} ✓.

And (1,1)^c: (λ^c)₁ = 2 - 1 = 1, (λ^c)₂ = 2 - 1 = 1. So (1,1)^c = (1,1). Also self-complementary. σ_{1,1}² = σ_{2,2} ✓.

And σ₂ · σ_{1,1} = 0 confirms that σ₂ and σ_{1,1} are NOT Poincaré dual to each other, even though they have the same codimension. The duality pairing is "diagonal" in a non-obvious basis.

---

## Stage 6: Grassmannians and ShaperOS

### Exercise 6.1: Choosing the Grassmannian

**Design question:** An agent has 3 independent capabilities in a system with 6 possible capability types. What Grassmannian models the agent's namespace?

**Answer:** Gr(3,6). The agent's namespace is a 3-dimensional subspace of a 6-dimensional capability space. Dimension = 3·3 = 9 (a 9-parameter family of possible configurations).

**Follow-up:** How many Schubert cells does Gr(3,6) have?

Count: number of partitions fitting in a 3×3 box. These are partitions (λ₁, λ₂, λ₃) with 3 ≥ λ₁ ≥ λ₂ ≥ λ₃ ≥ 0.

List them systematically:
- |λ| = 0: (0,0,0) — 1
- |λ| = 1: (1,0,0) — 1
- |λ| = 2: (2,0,0), (1,1,0) — 2
- |λ| = 3: (3,0,0), (2,1,0), (1,1,1) — 3
- |λ| = 4: (3,1,0), (2,2,0), (2,1,1) — 3
- |λ| = 5: (3,2,0), (3,1,1), (2,2,1) — 3
- |λ| = 6: (3,3,0), (3,2,1), (2,2,2) — 3
- |λ| = 7: (3,3,1), (3,2,2) — 2
- |λ| = 8: (3,3,2) — 1
- |λ| = 9: (3,3,3) — 1

Total: 1+1+2+3+3+3+3+2+1+1 = 20 = C(6,3). ✓ (The number of Schubert cells of Gr(k,n) is always C(n,k).)

### Exercise 6.2: Capability Codimension

**Interpret the codimension of a capability condition:**

In Gr(3,6), the Schubert classes of codimension 1 are σ₁ only (partition (1)). This represents "the namespace has nontrivial intersection with a fixed 3-plane."

Codimension 1 conditions are "mild" — they cut the 9-dimensional configuration space down by 1 dimension each. You need 9 such conditions (σ₁⁹) for a finite answer.

**Compute σ₁⁹ in Gr(3,6):** Use the hook-length formula for the 3×3 rectangle.

Hook lengths for the 3×3 grid:
```
(1,1): 2+2+1=5  (1,2): 1+2+1=4  (1,3): 0+2+1=3
(2,1): 2+1+1=4  (2,2): 1+1+1=3  (2,3): 0+1+1=2
(3,1): 2+0+1=3  (3,2): 1+0+1=2  (3,3): 0+0+1=1
```

Product: 5·4·3·4·3·2·3·2·1 = 5·4·3·4·3·2·3·2·1.

Compute step by step: 5·4 = 20, ·3 = 60, ·4 = 240, ·3 = 720, ·2 = 1440, ·3 = 4320, ·2 = 8640, ·1 = 8640.

deg = 9!/8640 = 362880/8640 = 42.

**σ₁⁹ = 42 in Gr(3,6).** A Catalan number again! (C₄ = 14... wait, 42 = C₅? No, C₅ = 42. Yes!)

**ShaperOS interpretation:** "Nine basic capability conditions on a 3-out-of-6 namespace yield exactly 42 valid configurations." This is the exact count that the Shaper Compiler would return.

### Exercise 6.3: Matroid Reading

**Connect to the matroid module:** The matroid of a point V ∈ Gr(3,6) records which 3-element subsets of {1,...,6} give nonzero Plücker coordinates (which triples of basis vectors project nontrivially onto V).

A generic point has all C(6,3) = 20 Plücker coordinates nonzero → uniform matroid U(3,6).

**Exercise:** For V = span(e₁, e₂, e₃), which Plücker coordinates are nonzero?

The 3×6 matrix is [I₃ | 0₃], so the only nonzero 3×3 minor is the first three columns: p₁₂₃ = 1, all others = 0.

This is the **Schubert matroid** for the partition (3,3,3) (the point class) — the most constrained matroid, with only one basis.

For V = span(e₁ + e₄, e₂ + e₅, e₃ + e₆):

Matrix: [1 0 0 1 0 0; 0 1 0 0 1 0; 0 0 1 0 0 1]

Which 3×3 minors are nonzero? Any three columns that give a nonsingular submatrix. Because of the identity block structure, a minor is nonzero as long as the three columns don't create a zero row. This is a more interesting matroid — work out its bases.

**Exercise:** Determine the circuits of this matroid (minimal dependent sets) and interpret them as "redundant capability groups" in ShaperOS.

### Exercise 6.4: Localization in Small Cases

**Tie in the equivariant localization path:**

For Gr(2,4), the torus T = (ℂ*)⁴ has C(4,2) = 6 fixed points. These are the coordinate 2-planes: span(eᵢ, eⱼ) for each {i,j} ⊂ {1,2,3,4}.

The localization formula says:

σ₁⁴ = Σ_{|I|=2} [σ₁]⁴(eᵢ) / e_T(T_I Gr)

where eᵢ = span(eᵢ₁, eᵢ₂) for I = {i₁, i₂}.

**Exercise:** Using standard weights t₁ = 1, t₂ = 2, t₃ = 3, t₄ = 4:

For each fixed point I, compute:
1. [σ₁]^T(eᵢ) = ∏_{box (a,b) in (1)} (t_{iₐ} − t_{jᵦ}) where {j₁,j₂} = [4]\I
2. The tangent Euler class e_T = ∏_{i∈I, j∉I} (tᵢ − tⱼ)
3. The contribution [σ₁]⁴/e_T

Sum all 6 contributions and verify the total is 2.

**This is a concrete numerical exercise.** Do it by hand for at least 2-3 fixed points, then complete the rest.

Fixed point I = {1,2}: J = {3,4}, weights tᵢ = (1,2), tⱼ = (3,4).

[σ₁]^T = (t₁ − t₁) ... hmm, I need to recall the equivariant Schubert class formula.

For σ₁ (partition (1), single box at position (1,1)):
[σ₁]^T(e_I) = ∏_{box (a,b) in (1)} (t_{i_{k-a}} − t_{j_{b}})

For k=2, partition (1) has one box at (a,b) = (1,1). So:
[σ₁]^T(e_I) = t_{i_{2-1}} − t_{j_1} = t_{i_1} − t_{j_1}

Wait, I need to be careful with the indexing. Let I = {i₁ < i₂}, J = {j₁ < j₂}.

For k=2, the formula gives [σ₁]^T(e_I) = t_{i_{k+1-a}} − t_{j_{b+1}} for each box (a,b). The partition (1) has one box at a=1 (first row), and b ranges from 0 to λ₁-1 = 0. So b=0.

[σ₁]^T(e_I) = t_{i_{2}} - t_{j₁}

(using 1-indexed: i_{k+1-1} = i_k = i₂, and j_{0+1} = j₁)

For I = {1,2}, J = {3,4}: [σ₁]^T = t₂ − t₃ = 2 − 3 = −1. Fourth power: (−1)⁴ = 1.

Tangent Euler: ∏_{i∈I, j∈J} (tᵢ − tⱼ) = (1−3)(1−4)(2−3)(2−4) = (−2)(−3)(−1)(−2) = 12.

Contribution: 1/12.

**Continue for all 6 fixed points, then sum.** The total should be 2. This is the localization path that `amari-enumerative` implements.

---

## Meta-Exercises (Ongoing)

### G1: Grassmannian Journal

For every ShaperOS design decision involving capability spaces, record:
- How many capability types? → n
- How many capabilities per agent? → k
- Which Grassmannian? → Gr(k,n)
- What Schubert conditions arise? → partitions
- What intersection number is relevant? → compute or look up

### G2: Cross-Check Discipline

Every intersection number you compute by one method, verify by another:
- LR tableaux ↔ Pieri rule
- Hook-length formula ↔ LR expansion
- Localization ↔ LR
- Small cases ↔ direct geometric enumeration

The agreement is the source of confidence. Disagreement means a bug (in your computation or in `amari-enumerative`).

### G3: Upgrading Grassmannians

When Gr(k,n) becomes too small for a design problem, identify why:
- Need more capability types? → increase n
- Need more capabilities per agent? → increase k
- Need richer structure (not just subspaces)? → consider flag varieties F(k₁,...,kₘ; n) or other homogeneous spaces

The flag variety F(1,2; 4) (flags of a line inside a 2-plane in ℝ⁴) already appears implicitly in ShaperOS when capabilities have dependency chains (capability A requires capability B).

---

## Appendix: Key Formulas

### Dimension
dim Gr(k,n) = k(n−k)

### Number of Schubert cells
C(n,k) (one per k-element subset, or equivalently, per partition in k × (n−k) box)

### Degree (σ₁^{k(n-k)})
Hook-length formula for the k × (n−k) rectangle:
deg = (k(n−k))! / ∏_{(i,j)} hook(i,j)
where hook(i,j) = (n−k−j) + (k−i) + 1 = n + 1 − i − j

### Pieri Rule
σ_p · σ_λ = Σ σ_μ
Sum over μ ⊃ λ with |μ| = |λ| + p and μ/λ a horizontal strip (no two boxes in the same column).

### Giambelli Formula
Any Schubert class σ_λ can be expressed as a determinant of special Schubert classes:
σ_λ = det(σ_{λᵢ−i+j})_{1≤i,j≤k}

For example, σ_{2,1} = det[σ₂ σ₃; σ₀ σ₁] = σ₂σ₁ − σ₃σ₀ = σ₂σ₁ − σ₃.
(In Gr(2,4), σ₃ = 0 since max codim per row is n−k = 2, so σ_{2,1} = σ₂σ₁.)
Verify: σ₂ · σ₁ = σ_{2,1} from our table. ✓

### Duality
Gr(k,n) ≅ Gr(n−k,n). Under this isomorphism, σ_λ ↦ σ_{λ^c} where λ^c is the complement in the k × (n−k) box.

### Plücker Embedding
Gr(k,n) → ℙ(∧ᵏℝⁿ) ≅ ℝP^{C(n,k)−1}
V = span(v₁,...,vₖ) ↦ [v₁ ∧ ··· ∧ vₖ]
In GA: V ↦ grade-k blade in Cl(n,0,0)
