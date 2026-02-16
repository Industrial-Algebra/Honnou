# Signature Intuition: A Progressive Exercise Set for Geometric Algebra

**Companion to:** Hestenes, *New Foundations for Classical Mechanics*
**Prerequisite:** Familiarity with the geometric product, blades, and grade structure
**Goal:** Develop the ability to predict the correct Clifford algebra signature Cl(p,q,r) for a given problem domain, and understand the geometric consequences of getting it wrong

---

## How to Use This Document

Each stage contains exercises organized as **Predict → Compute → Reflect**:

1. **Predict**: Before computing anything, write down what you expect. This is the muscle you're training.
2. **Compute**: Work it out explicitly. Keep computations in a notebook — the physical act of writing matters.
3. **Reflect**: Compare prediction to result. When they disagree, that's where learning happens. Write a sentence about *why* your intuition was wrong.

**Signature journal**: Keep a running log. For every new domain you encounter (a paper, an Amari module, a physics problem), write your first-instinct signature before analyzing it. Review monthly. Your calibration will visibly improve.

---

## Stage 1: Consequences of a Single Sign

### Foundations

In Cl(p,q,r), basis vectors satisfy:

- eᵢ² = +1 for i = 1, ..., p (positive/spacelike)
- eⱼ² = −1 for j = p+1, ..., p+q (negative/timelike)
- eₖ² = 0 for k = p+q+1, ..., p+q+r (degenerate/null)

The geometric product of two vectors a, b decomposes as:

ab = a·b + a∧b

where a·b is the inner product (scalar, grade 0) and a∧b is the outer product (bivector, grade 2). The signature determines the inner product, which determines everything downstream.

### Exercise 1.1: Two Vectors in Three Signatures

Let a = e₁ and b = cos(θ)e₁ + sin(θ)e₂ for θ = π/4.

**In Cl(2,0,0):** Both basis vectors square to +1.

**Predict:** What is ab? What is (ab)²? Is ab invertible? What transformation does x ↦ (ab)x(ab)⁻¹ perform?

**Compute:**

```
a = e₁
b = (1/√2)e₁ + (1/√2)e₂

ab = e₁((1/√2)e₁ + (1/√2)e₂)
   = (1/√2)e₁² + (1/√2)e₁e₂
   = (1/√2) + (1/√2)e₁₂

(ab)² = ((1/√2) + (1/√2)e₁₂)²
      = 1/2 + 2·(1/√2)·(1/√2)·e₁₂ + (1/2)·e₁₂²
      = 1/2 + e₁₂ + (1/2)(e₁e₂e₁e₂)
      = 1/2 + e₁₂ + (1/2)(−e₁e₁e₂e₂)    [anticommute e₂e₁ = −e₁e₂]
                                              [wait — more carefully:]
```

Actually let's be more careful. e₁₂² = e₁e₂e₁e₂ = −e₁e₁e₂e₂ = −(+1)(+1) = −1 in Cl(2,0,0).

```
(ab)² = 1/2 + e₁₂ + (1/2)(−1)
      = e₁₂
```

So (ab)² = e₁₂, a pure bivector. And e₁₂² = −1, so (ab)⁴ = −1, (ab)⁸ = +1. This is a rotor generating rotation — it has order 8 in this case because θ = π/4 and the sandwich product doubles the angle.

ab is invertible because (ab)(ba) = a(bb)a = a(b·b)a = a·(1)·a = a² = 1 (since b·b = cos²θ + sin²θ = 1 in this signature).

**Now repeat in Cl(1,1,0):** e₁² = +1, e₂² = −1.

**Predict first**, then compute:

```
ab = (1/√2) + (1/√2)e₁₂

e₁₂² = e₁e₂e₁e₂ = −e₁e₁e₂e₂ = −(+1)(−1) = +1
```

Now e₁₂² = +1 instead of −1. This changes everything:

```
(ab)² = 1/2 + e₁₂ + 1/2 = 1 + e₁₂
(ab)⁴ = (1 + e₁₂)² = 1 + 2e₁₂ + 1 = 2 + 2e₁₂
```

This doesn't cycle — it *grows*. The "rotation" is now a hyperbolic boost. The bivector e₁₂ generates hyperbolic rotations when it squares to +1.

Also: b·b = cos²θ·(+1) + sin²θ·(−1) = cos²θ − sin²θ = cos(2θ). At θ = π/4, b·b = 0. The vector b is **null** in this signature. ab is still defined but b is not invertible.

**Now in Cl(0,2,0):** e₁² = −1, e₂² = −1.

```
ab = (1/√2)e₁² + (1/√2)e₁e₂
   = −(1/√2) + (1/√2)e₁₂

e₁₂² = −(−1)(−1) = −1
```

Same e₁₂² = −1 as Cl(2,0,0), so this generates a rotation too. But the scalar part flipped sign: the rotor is −(1/√2) + (1/√2)e₁₂ instead of +(1/√2) + (1/√2)e₁₂. The rotation is in the opposite sense — or equivalently, the "angle" interpretation requires care because the inner product has flipped sign.

**Reflect:** Fill in this table from your computations:

| Signature | e₁₂² | ab invertible? | b null? | Transformation type |
|-----------|-------|---------------|---------|-------------------|
| Cl(2,0,0) | −1 | Yes | No | Rotation (elliptic) |
| Cl(1,1,0) | +1 | Yes | Yes (at θ=π/4) | Boost (hyperbolic) |
| Cl(0,2,0) | −1 | Yes | No | Rotation (elliptic, reversed) |

**Key insight:** The transformation type is determined by whether e₁₂² = −1 (elliptic/rotation) or +1 (hyperbolic/boost). This is the single most important piece of signature intuition.

### Exercise 1.2: The Pseudoscalar

For each of Cl(2,0,0), Cl(1,1,0), Cl(0,2,0), compute the pseudoscalar I = e₁e₂ = e₁₂ and determine I².

**Predict:** In Cl(p,q,0) with n = p+q, does I² = +1 or −1? Find the general formula.

**Compute and verify:**

I² = e₁e₂e₁e₂ = (−1)^(number of anticommutations) · ∏ eᵢ²

The sign from anticommuting is (−1)^(n(n-1)/2) and the product of squared basis vectors is (−1)^q.

So I² = (−1)^(n(n-1)/2 + q).

| Algebra | n | n(n-1)/2 | q | n(n-1)/2 + q | I² |
|---------|---|----------|---|-------------|-----|
| Cl(2,0,0) | 2 | 1 | 0 | 1 | −1 |
| Cl(1,1,0) | 2 | 1 | 1 | 2 | +1 |
| Cl(0,2,0) | 2 | 1 | 2 | 3 | −1 |
| Cl(3,0,0) | 3 | 3 | 0 | 3 | −1 |
| Cl(2,1,0) | 3 | 3 | 1 | 4 | +1 |
| Cl(1,2,0) | 3 | 3 | 2 | 5 | −1 |
| Cl(3,1,0) | 4 | 6 | 1 | 7 | −1 |
| Cl(1,3,0) | 4 | 6 | 3 | 9 | −1 |

**Key insight:** I² determines whether the Hodge dual is an involution (I² = +1) or an anti-involution (I² = −1). This matters for ShaperOS because the meet operation a ∨ b = ⋆(⋆a ∧ ⋆b) depends on the Hodge star, which depends on I.

### Exercise 1.3: Inverse Existence

**Predict, then verify:** For which of the following is the element v = 3e₁ + 4e₂ invertible?

(a) Cl(2,0,0): v² = 9(+1) + 24e₁₂ + 16(+1) — wait, that's wrong. v² = v·v + v∧v. For a vector, v² = v·v (the outer product of a vector with itself is zero). So v² = 9e₁² + 16e₂² = 9(+1) + 16(+1) = 25. Invertible, v⁻¹ = v/25.

(b) Cl(1,1,0): v² = 9(+1) + 16(−1) = 9 − 16 = −7. Invertible (nonzero), v⁻¹ = v/(−7) = −v/7. Note: the inverse exists but has opposite sign. The vector is "timelike" (negative norm).

(c) Cl(0,2,0): v² = 9(−1) + 16(−1) = −25. Invertible, v⁻¹ = v/(−25) = −v/25.

Now try v = 3e₁ + 4e₂ where 3² · s₁ + 4² · s₂ = 0 (sᵢ is the sign of eᵢ²):

(d) Cl(1,1,0) with v = 4e₁ + 4e₂: v² = 16(+1) + 16(−1) = 0. **Not invertible.** This vector is **null** — it lies on the light cone of the (1,1) metric. Null vectors are the geometric reason physicists care about Minkowski signature.

**Key insight:** A vector is invertible iff its square is nonzero. In Cl(p,q,0), null vectors exist iff q > 0 (or p > 0, depending on convention). The null cone is the boundary between "rotations" and "boosts."

### Exercise 1.4: The Signature Zoo (Quick Drills)

For each algebra, determine the stated property. Work them all, then check.

| Algebra | Property to determine |
|---------|---------------------|
| Cl(3,0,0) | Is e₁₂₃ a square root of −1? |
| Cl(0,3,0) | Is e₁₂₃ a square root of −1? |
| Cl(4,0,0) | Does the pseudoscalar commute with all elements? |
| Cl(3,1,0) | How many independent null vectors exist? |
| Cl(2,2,0) | What is the maximum dimension of a totally null subspace? |
| Cl(1,0,0) | Is this algebra isomorphic to ℝ ⊕ ℝ or ℂ? |
| Cl(0,1,0) | Is this algebra isomorphic to ℝ ⊕ ℝ or ℂ? |

**Answers and reasoning:**

- Cl(3,0,0): I = e₁₂₃. I² = (−1)^(3·2/2 + 0) = (−1)^3 = −1. Yes, I² = −1.
- Cl(0,3,0): I² = (−1)^(3 + 3) = (−1)^6 = +1. No — I is a square root of +1.
- Cl(4,0,0): The pseudoscalar commutes with all elements iff n is even. n = 4, so yes. (A grade-n element commutes with grade-k elements when n is even, anticommutes when n is odd.)
- Cl(3,1,0): A null vector v satisfies v² = 0, i.e., Σ aᵢ²sᵢ = 0. With signature (+,+,+,−), solutions form a 2-dimensional cone (the "light cone" in 3+1 dimensions). The cone isn't a subspace, but maximal totally null subspaces have dimension min(p,q) = 1.
- Cl(2,2,0): max totally null = min(2,2) = 2. You can find a 2D subspace where every vector is null and every pair of vectors is orthogonal. This is the split signature — it arises in twistor theory and has qualitatively different geometry from (3,1) or (1,3).
- Cl(1,0,0): e₁² = +1. Algebra has dimension 2, basis {1, e₁}. Since e₁² = 1, the algebra splits: set e± = (1 ± e₁)/2, then e+² = e+, e−² = e−, e+e− = 0. Isomorphic to ℝ ⊕ ℝ.
- Cl(0,1,0): e₁² = −1. Algebra has dimension 2, basis {1, e₁}. This *is* ℂ, with e₁ playing the role of i.

**Key insight:** Cl(1,0,0) ≅ ℝ ⊕ ℝ (splits) while Cl(0,1,0) ≅ ℂ (doesn't split). This is the simplest example of how a single sign flip changes the algebra's entire structure. The pattern — positive squares split, negative squares give division algebras — repeats throughout the Bott periodicity table.

---

## Stage 2: The Degenerate Dimension

### Motivation

Degenerate dimensions (eₖ² = 0) are the least intuitive but arguably the most useful for applications. They give you projective geometry, homogeneous coordinates, and "ideal elements" (points at infinity). In ShaperOS, degenerate dimensions can model forgotten memories, revoked capabilities, or limit cases.

### Exercise 2.1: From Euclidean to Projective

Start in Cl(2,0,0) — the Euclidean plane.

**Problem:** Represent two lines ℓ₁ and ℓ₂. Compute their intersection.

In Cl(2,0,0), a line through the origin can be represented as a vector (its normal direction). But a *general* line (not through the origin) can't be represented as a single algebraic element — you need an offset, which breaks the algebra's natural structure.

**Now add a degenerate dimension:** Move to Cl(2,0,1) with e₃² = 0.

**Represent a general line** as a bivector: ℓ = ae₁₃ + be₂₃ + ce₁₂, where ax + by + c = 0 is the line equation. The degenerate dimension e₃ represents the "ideal point" or "homogeneous weight."

Given: ℓ₁: x + y − 1 = 0 and ℓ₂: x − y + 1 = 0.

```
ℓ₁ = e₁₃ + e₂₃ − e₁₂     (a=1, b=1, c=−1)
ℓ₂ = e₁₃ − e₂₃ + e₁₂     (a=1, b=−1, c=1)
```

**Compute the intersection** using the regressive product (meet):

ℓ₁ ∨ ℓ₂ = ⋆(⋆ℓ₁ ∧ ⋆ℓ₂)

First, find the Hodge duals. In Cl(2,0,1) with pseudoscalar I = e₁₂₃:

**Pause.** There's a subtlety: the pseudoscalar is degenerate (I² = e₁₂₃² involves e₃² = 0, making I non-invertible). The standard Hodge dual requires I⁻¹, which doesn't exist.

**This is the exercise.** You've hit the wall that degenerate dimensions create. The way through:

Option A: Use the Poincaré dual instead (which doesn't require invertibility).
Option B: Work in the dual algebra and use the "join" of the dual elements.
Option C: Use the shuffle product formulation of the meet that doesn't invoke the Hodge star.

For this exercise, use the explicit meet formula for bivectors in 3D. In general, for two bivectors B₁, B₂ in a 3D algebra, their meet is:

ℓ₁ ∨ ℓ₂ = (ℓ₁ ⌋ I⁻¹) ∧ ℓ₂

But I isn't invertible! So instead, use the left contraction with a non-degenerate pseudoscalar substitute, or compute directly:

The point of intersection of two lines in projective 2-space: take the "cross product" of the line coordinates.

```
p = ℓ₁ × ℓ₂ = (1·1 − (−1)·(−1), (−1)·1 − 1·1, 1·(−1) − 1·1)
  = (1 − 1, −1 − 1, −1 − 1)
  = (0, −2, −2)
```

Dehomogenize: (x, y) = (0/(−2), (−2)/(−2)) = (0, 1).

**Verify:** x + y − 1 = 0 + 1 − 1 = 0 ✓ and x − y + 1 = 0 − 1 + 1 = 0 ✓.

**Reflect:** The degenerate dimension e₃ gave us homogeneous coordinates. But it also made the pseudoscalar non-invertible, which broke the naive Hodge dual. This is a fundamental tradeoff of degenerate dimensions: you gain projective structure but lose certain algebraic operations.

### Exercise 2.2: Parallel Lines

Using the same Cl(2,0,1) setup:

ℓ₁: x + y − 1 = 0 → ℓ₁ = e₁₃ + e₂₃ − e₁₂
ℓ₃: x + y − 3 = 0 → ℓ₃ = e₁₃ + e₂₃ − 3e₁₂

These lines are parallel. Compute ℓ₁ × ℓ₃:

```
p = (1·(−3) − (−1)·1, (−1)·1 − 1·(−3), 1·1 − 1·1)
  = (−3 + 1, −1 + 3, 0)
  = (−2, 2, 0)
```

The third coordinate is 0 — this is a **point at infinity** (ideal point). It represents the direction (−2, 2) ∝ (−1, 1), which is perpendicular to the direction (1, 1) of the parallel lines.

**Key insight:** Parallel lines intersect at a point at infinity, represented by a vector with zero e₃-component. The degenerate dimension's entire purpose is to distinguish "finite intersection" (nonzero weight) from "ideal intersection" (zero weight). Without it, parallel lines simply don't intersect and the algebra gives no answer.

### Exercise 2.3: What Breaks When You Promote

**Predict:** Take the parallel-lines example and replace Cl(2,0,1) with Cl(2,1,0) (promote the degenerate dimension to negative). What changes?

**Compute:**

Now e₃² = −1 instead of 0. The pseudoscalar I = e₁₂₃ satisfies I² = (−1)^(3·2/2 + 1) = (−1)^4 = +1. So I is invertible — good for Hodge duals, but we've lost the projective structure.

With e₃² = −1, the "line" ℓ₁ = e₁₃ + e₂₃ − e₁₂ is still a bivector, but its geometric meaning has changed. In Cl(2,1,0), bivectors represent oriented planes in a 3D space with Minkowski-like metric, not lines in a projective plane.

The "point at infinity" (−2, 2, 0) is now just a regular vector with norm (−2)²·1 + 2²·1 + 0²·(−1) = 8 — a perfectly ordinary spacelike vector, not an ideal element at all.

**Key insight:** Promoting a degenerate dimension to nondegenerate collapses the projective structure. Ideal elements become ordinary elements; the distinction between "finite" and "at infinity" disappears. The algebraic operations still work, but their geometric interpretation changes completely.

### Exercise 2.4: Building PGA from Scratch

**Goal:** Derive the Projective Geometric Algebra (PGA) for 3D space. Don't look up the answer — derive the signature from requirements.

**Requirements:**
1. Must represent points, lines, and planes in 3D space
2. Must handle parallel lines (intersect at infinity)
3. Must represent both "finite" and "ideal" elements
4. Rotations and translations should be versors

**Derivation:**

Step 1: 3D Euclidean space needs 3 spatial dimensions. Start with e₁, e₂, e₃ squaring to +1.

Step 2: Requirement 2 demands ideal elements, which need a degenerate dimension (Exercise 2.2 showed why). Add e₀ with e₀² = 0.

Step 3: Check that translations work. A translation T_v by vector v = v₁e₁ + v₂e₂ + v₃e₃ should be a versor. In PGA, the translator is T = 1 + (1/2)(v₁e₀₁ + v₂e₀₂ + v₃e₀₃). Verify: T x T̃ shifts points by v. (This works because e₀² = 0 makes T² = 1 + v₁e₀₁ + ... , and the degenerate dimension prevents higher-order terms.)

**Result:** Cl(3,0,1). This is PGA for 3D.

**Now predict:** What goes wrong if you use Cl(3,1,0) instead? (Answer: translations aren't nilpotent — T² ≠ 1 + linear terms, so you get a different group of motions. Specifically, you get the conformal group rather than the Euclidean group.)

### Exercise 2.5: Multiple Degenerate Dimensions

**Question:** When would you want Cl(p,q,r) with r > 1?

This is an open-ended thinking exercise. Consider:

- Cl(n,0,2): Two independent "infinities." Could model a system with two distinct limit behaviors (e.g., spatial infinity and temporal infinity; or two independent quotient structures).
- Cl(0,0,n): Everything is degenerate. This is the exterior algebra ∧ℝⁿ (no metric at all). The geometric product reduces to the exterior product for basis vectors. This is what you'd use when you care only about linear independence and orientation, not lengths or angles.

**For ShaperOS:** A revoked capability might become a null vector (degenerate). If capabilities can be revoked along multiple independent "dimensions of trust," you might want multiple degenerate dimensions. But this makes the algebra harder to work with (more non-invertible elements, Hodge dual issues). The tradeoff is expressiveness vs. algebraic tractability.

---

## Stage 3: The Conformal Embedding

### Motivation

The Conformal Geometric Algebra (CGA) embeds Euclidean n-space into Cl(n+1,1,0). This is the most "non-obvious" signature choice in practical GA: you add two dimensions, one positive and one negative, and suddenly circles and spheres become first-class algebraic objects. Understanding *why* this specific signature works (and others don't) is the deepest test of signature intuition.

### Exercise 3.1: Why Not Cl(3,0,0) for Circles?

In the Euclidean plane Cl(2,0,0), try to represent a circle of radius r centered at point c.

**Attempt:** A circle is a 1D curve in 2D space. There's no single blade that represents it — a blade represents a *flat* subspace (point, line, or plane), never a curved object.

You could represent the circle parametrically: p(θ) = c + r(cos(θ)e₁ + sin(θ)e₂). But this is a *function*, not an algebraic element. You can't compute "intersection of two circles" with the geometric product.

**Key insight:** Flat subspaces are blades. Curved subspaces aren't. To make circles algebraic, you need to find a space where circles *become* flat — i.e., where circles are intersections of hyperplanes with something.

### Exercise 3.2: The Null Cone Embedding

The CGA trick: embed ℝ² into the null cone of ℝ³˒¹ (3 positive, 1 negative dimensions).

Add two new basis vectors: e₊ with e₊² = +1 and e₋ with e₋² = −1. Define:

```
e∞ = e₋ + e₊    (point at infinity)
e₀ = (e₋ − e₊)/2    (origin)
```

**Compute:**

```
e∞² = (e₋ + e₊)² = e₋² + e₋e₊ + e₊e₋ + e₊²
     = (−1) + e₋e₊ − e₋e₊ + (+1) = 0

e₀² = ((e₋ − e₊)/2)² = (e₋² − e₋e₊ − e₊e₋ + e₊²)/4
     = (−1 − e₋e₊ + e₋e₊ + 1)/4 = 0

e∞ · e₀ = (e₋ + e₊) · (e₋ − e₊)/2 = (e₋² − e₊²)/2 = (−1 − 1)/2 = −1
```

Both e∞ and e₀ are **null vectors**, and their inner product is −1. These two null vectors, carved from one positive and one negative dimension, are the entire mechanism.

**Map a Euclidean point x = x₁e₁ + x₂e₂ to CGA:**

```
X = x + (1/2)x²e∞ + e₀
```

**Verify X is null:**

```
X² = x² + x·(x²e∞) + x·e₀ + (x²e∞)·x + (1/4)x⁴e∞² + (1/2)x²e∞·e₀ + e₀·x + (1/2)x²e₀·e∞ + e₀²
   = x² + 0 + 0 + 0 + 0 + (1/2)x²(−1) + 0 + (1/2)x²(−1) + 0
```

Wait — let me be more careful. For vectors in the full space:

```
X · X = x·x + 2·(x)·((1/2)x²e∞) + 2·(x)·(e₀) + 2·((1/2)x²e∞)·(e₀) + (1/2)²x⁴·e∞·e∞ + e₀·e₀
```

Since x is in the Euclidean subspace, x·e∞ = 0, x·e₀ = 0 (orthogonal subspaces). So:

```
X · X = x·x + 2·(1/2)x²·(e∞·e₀) + 0 + 0
      = x² + x²·(−1)
      = 0
```

X is null. Every Euclidean point maps to a null vector in CGA. The null cone of Cl(3,1,0) *is* the Euclidean plane (up to this embedding).

### Exercise 3.3: Why This Signature and No Other

**The key question:** We needed two extra dimensions, one squaring to +1 and one to −1. What happens with other choices?

**Case A: Cl(4,0,0) — both extra dimensions positive.**

Try e₊² = +1, e₊'² = +1. Define e∞ = e₊ + e₊' and e₀ = (e₊ − e₊')/2.

```
e∞² = 1 + e₊e₊' + e₊'e₊ + 1 = 2 + 0 = 2 ≠ 0
```

e∞ is not null. The embedding breaks — there's no null cone in a positive-definite space. No null cone means no projective structure, no points at infinity, no way to make circles flat.

**Case B: Cl(2,2,0) — both extra dimensions negative.**

Try e₋² = −1, e₋'² = −1. Define e∞ = e₋ + e₋' and e₀ = (e₋ − e₋')/2.

```
e∞² = −1 + e₋e₋' + e₋'e₋ + (−1) = −2 ≠ 0
```

Same problem — not null.

**Case C: Cl(3,0,1) — one degenerate instead of one negative.**

Try e₊² = +1, e₀² = 0 (PGA-style). Now e∞ = e₊ + e₀:

```
e∞² = 1 + e₊e₀ + e₀e₊ + 0 = 1 ≠ 0
```

Not null either.

**Case D: Cl(2,0,2) — both degenerate.**

e₃² = 0, e₄² = 0. e∞ = e₃ + e₄:

```
e∞² = 0 + e₃e₄ + e₄e₃ + 0 = 0
```

Null! But check: e₀ = (e₃ − e₄)/2, e₀² = 0. And e∞·e₀ = (e₃² − e₄²)/2 = 0. The null vectors are orthogonal, so e∞·e₀ = 0 instead of −1. The embedding won't work — you need e∞·e₀ = −1 to normalize properly.

**Only Cl(n+1,1,0) (or equivalently Cl(1,n+1,0)) works.** You need exactly one positive and one negative extra dimension to create a null pair with nonzero inner product. This is the conformal signature.

**Reflect:** The conformal trick works because of a coincidence in the null cone structure: you need null vectors that are *not orthogonal*. This requires mixed signature. No other combination of signs gives you this.

### Exercise 3.4: Circles as Blades

In CGA for the plane (Cl(3,1,0)), a circle through three points P₁, P₂, P₃ is:

C = X₁ ∧ X₂ ∧ X₃

where Xᵢ are the CGA embeddings of the points.

**Compute:** Find the circle through (1,0), (0,1), (−1,0).

```
X₁ = e₁ + (1/2)e∞ + e₀
X₂ = e₂ + (1/2)e∞ + e₀
X₃ = −e₁ + (1/2)e∞ + e₀
```

The outer product X₁ ∧ X₂ ∧ X₃ is a grade-3 blade in a 4D algebra (dimension 2⁴ = 16). Computing it fully is a good exercise in bookkeeping. The result will be a trivector that represents the unit circle centered at (0, 1/2) ... actually, let me not spoil it. 

**The exercise:** Compute this wedge product explicitly. Then verify that the circle you get passes through all three points by checking X₁ ∧ C = 0, X₂ ∧ C = 0, X₃ ∧ C = 0 (a point lies on a circle iff it's linearly dependent with the circle's defining points).

**The deeper exercise:** Two circles intersect when their meet is nonzero. Define a second circle through (0,1), (1,0), (0,−1) and compute the meet. The result should be a point pair (the two intersection points).

### Exercise 3.5: The CGA Signature for Higher Dimensions

**Predict:** What signature do you need for CGA in 3D (representing spheres, circles, and points in ℝ³)?

**Answer:** Cl(4,1,0). You embed ℝ³ into the null cone of ℝ⁴˒¹. The algebra has dimension 2⁵ = 32. A sphere is a grade-4 blade (four points determine a sphere), a circle is a grade-3 blade, a point pair is grade-2.

**General rule:** CGA for ℝⁿ uses Cl(n+1,1,0). The algebra dimension is 2^(n+2), which grows fast. For ℝ³ it's manageable (32D), for ℝ⁴ it's 64D, and beyond that you need sparse representations.

---

## Stage 4: Minkowski vs. Anti-Minkowski

### Motivation

The choice between Cl(1,3,0) and Cl(3,1,0) for spacetime is the longest-running convention war in mathematical physics. Both give correct physics. The differences are entirely in the intermediate algebra. Understanding exactly where the differences surface — and where they don't — is a signature mastery test.

### Exercise 4.1: Electromagnetic Field Bivector

The electromagnetic field is a bivector F in spacetime algebra.

**In Cl(1,3,0)** (Hestenes convention, "particle physics" convention):
e₀² = +1 (time), e₁² = e₂² = e₃² = −1 (space).

```
F = E₁e₀₁ + E₂e₀₂ + E₃e₀₃ + B₁e₂₃ + B₂e₃₁ + B₃e₁₂
```

The electric part is the e₀ᵢ bivectors (time ∧ space); the magnetic part is the eᵢⱼ bivectors (space ∧ space).

**Compute F²:**

```
F² = (E² − B²) + 2(E⃗·B⃗)I
```

where I = e₀₁₂₃ is the pseudoscalar. This decomposes into scalar (the Lorentz invariant E² − B²) and pseudoscalar (the other invariant E⃗·B⃗).

**Now repeat in Cl(3,1,0)** (Doran-Lasenby convention, "general relativity" convention):
e₁² = e₂² = e₃² = +1 (space), e₀² = −1 (time).

```
F = E₁e₁₀ + E₂e₂₀ + E₃e₃₀ + B₁e₂₃ + B₂e₃₁ + B₃e₁₂
```

Note the index ordering: e₁₀ not e₀₁, because the conventional sign of the electric field components depends on the signature.

**Compute F²:** You should get:

```
F² = −(E² − B²) − 2(E⃗·B⃗)I
```

The physics is the same (the invariants E² − B² and E⃗·B⃗ are unchanged), but there's an overall sign flip in how they sit in the algebra.

**Where the difference matters:** Duality. In Cl(1,3,0), I² = +1, so the dual field F̃ = FI satisfies F̃̃ = FI² = F. Duality is an involution. In Cl(3,1,0), I² = −1, so F̃̃ = −F. Duality is an anti-involution. The Maxwell equations in "self-dual" form look different:

Cl(1,3,0): dF = J becomes d(E + IB) = J (Hestenes's form)
Cl(3,1,0): ∇F = J (Doran-Lasenby form)

Both are correct; the E + IB combination is natural in one convention, the ∇F form in the other.

### Exercise 4.2: Lorentz Boost

A Lorentz boost along e₁ with rapidity φ:

**In Cl(1,3,0):** The boost bivector is B = e₀₁. Check: B² = e₀e₁e₀e₁ = −e₀²e₁² = −(+1)(−1) = +1. Since B² > 0, the exponential exp(φB/2) generates a hyperbolic rotation (boost). The rotor is:

R = exp(φe₀₁/2) = cosh(φ/2) + sinh(φ/2)e₀₁

**In Cl(3,1,0):** B = e₁₀. B² = e₁e₀e₁e₀ = −e₁²e₀² = −(+1)(−1) = +1. Same! The boost bivector squares to +1 in both conventions.

R = exp(φe₁₀/2) = cosh(φ/2) + sinh(φ/2)e₁₀

**The physics is identical.** The rapidity φ, the cosh/sinh structure, and the transformation of 4-vectors are all the same. The only difference is a labeling convention.

### Exercise 4.3: Where the Choice Actually Matters

**Predict:** In which of the following situations does the Cl(1,3) vs Cl(3,1) choice produce a genuine difference (not just a sign convention)?

(a) Computing the energy-momentum of an electromagnetic field
(b) Finding eigenvalues of a Lorentz transformation
(c) Implementing the algebra computationally
(d) Defining spinor representations

**Analysis:**

(a) No genuine difference. Both give the same stress-energy tensor.

(b) No genuine difference. The eigenvalues of the boost are e^(±φ) in both.

(c) **Yes.** The Cayley table is different — you need different multiplication rules. A library that hardcodes Cl(1,3) can't be used for Cl(3,1) without changing the metric. In `amari-core`, the signature parameter (p,q,r) controls the Cayley table generation, so this is handled.

(d) **Yes.** The spinor space of Cl(1,3) ≅ M₂(ℂ) while Cl(3,1) ≅ M₂(ℍ) (2×2 matrices over quaternions vs. complex numbers). These are different algebraic structures — not just a sign convention. If you're implementing spinors concretely (as you might for agent belief states in ShaperOS), the representation theory differs.

**Key insight:** For classical physics (electrodynamics, mechanics), the choice is pure convention. For representation theory (spinors, K-theory), it's a genuine structural difference. This matters for ShaperOS's quantum K-theory module, where Chern characters and Adams operations depend on the representation ring.

---

## Stage 5: Signature for Information Geometry

### Motivation

This stage connects signature choice to your Amari library work. Statistical manifolds have natural geometric structure — the Fisher information metric — and the question of how to embed this in a Clifford algebra is open and interesting.

### Exercise 5.1: Fisher Metric of a Normal Distribution

The family of normal distributions N(μ, σ²) forms a 2D statistical manifold parameterized by θ = (μ, σ).

**Compute the Fisher information metric:**

```
g_ij = E[-∂²/∂θⁱ∂θʲ log p(x|θ)]

For N(μ,σ²):
log p = -(x-μ)²/(2σ²) - log(σ) - (1/2)log(2π)

g_μμ = 1/σ²
g_μσ = 0
g_σσ = 2/σ²
```

The metric tensor at (μ, σ) is diag(1/σ², 2/σ²). This is **positive definite** everywhere (both eigenvalues are positive).

**Natural signature:** Cl(2,0,0). Two vectors in the tangent space at any point have positive-definite inner product under Fisher.

**Embed:** Let e₁ correspond to the μ-direction and e₂ to the σ-direction. At point (μ₀, σ₀), a tangent vector v = aδμ + bδσ has squared norm:

```
|v|² = a²/σ₀² + 2b²/σ₀²
```

This is always positive. No null vectors, no timelike directions.

### Exercise 5.2: KL Divergence and Asymmetry

The Kullback-Leibler divergence D_KL(p‖q) is **not symmetric**: D_KL(p‖q) ≠ D_KL(q‖p).

**Compute:** For N(μ₁, σ₁²) and N(μ₂, σ₂²):

```
D_KL(p‖q) = log(σ₂/σ₁) + (σ₁² + (μ₁-μ₂)²)/(2σ₂²) - 1/2
```

Specific example: p = N(0,1), q = N(1,1):
D_KL(p‖q) = 0 + (1 + 1)/2 - 1/2 = 1/2
D_KL(q‖p) = 0 + (1 + 1)/2 - 1/2 = 1/2

(These happen to be equal because σ₁ = σ₂. Try p = N(0,1), q = N(0,2):)

D_KL(p‖q) = log(2) + 1/(2·4) - 1/2 = log(2) - 3/8 ≈ 0.318
D_KL(q‖p) = log(1/2) + (4 + 0)/2 - 1/2 = −log(2) + 3/2 ≈ 0.807

**The asymmetry is real.** Can Cl(2,0,0) represent it?

**Attempt:** In Cl(2,0,0), the inner product is symmetric: a·b = b·a. The distance between two points is symmetric. There's no algebraic mechanism for asymmetry.

**Amari's insight:** The asymmetry comes from two different *connections* on the same manifold — the e-connection (exponential) and the m-connection (mixture). These are dual under the Fisher metric but distinct geometrically.

### Exercise 5.3: Mixed Signature for Dual Connections

**Speculative exercise:** Can an indefinite signature encode the dual connection structure?

Consider Cl(1,1,0) for the 1D case (just the σ parameter). The two null directions e₊ = (e₁ + e₂)/√2 and e₋ = (e₁ − e₂)/√2 satisfy e₊² = 0, e₋² = 0, e₊·e₋ = 1.

**Attempt:** Assign the e-connection to the e₊ direction and the m-connection to the e₋ direction. A "geodesic" in the e-connection goes along e₊; in the m-connection, along e₋.

The KL divergence from p to q goes along the e₊ null direction; from q to p along e₋. Asymmetry is now encoded in the distinction between the two null directions.

**Does this actually work?** Partially. The dual connection structure of information geometry does have a "null" character — the e-geodesic and m-geodesic from p to q, together with the metric geodesic, form a triangle with specific angle properties (Amari's generalized Pythagorean theorem). The null directions of Cl(1,1,0) capture the duality, but the full theory requires more structure (the cubic tensor, the α-connections for all α ∈ [−1, 1]).

**The honest conclusion:** There isn't a universally accepted Clifford algebra embedding for information geometry. The Fisher metric says Cl(n,0,0). The dual connection structure suggests indefinite signature or degenerate dimensions for the α ≠ 0 connections. This is an open research area.

**Reflect on the process:** The value of this exercise isn't the answer — it's the practice of translating geometric requirements into signature constraints, trying them, and discovering where they work and where they break.

### Exercise 5.4: Divergence as a Blade?

**Harder question:** Is there a way to represent D_KL(p‖q) as a blade coefficient in some Clifford algebra?

Hint: D_KL(p‖q) = ∫ p(x) log(p(x)/q(x)) dx. This is an expectation (integral against p), which is a linear functional. In the exterior algebra, linear functionals are grade-1 elements (covectors). The logarithmic ratio log(p/q) is the "score difference."

In a Clifford algebra over the function space, you could represent the score function s_p(x) = ∂log p/∂θ as a vector, and D_KL as an inner product of score vectors... but this requires an infinite-dimensional Clifford algebra over L²(p), which is well beyond standard GA.

**For ShaperOS:** The practical takeaway is that capability distances (how "far apart" two namespace configurations are) might naturally be asymmetric. If you model capability space with the Fisher geometry of agent belief distributions, the distance from configuration A to configuration B can differ from B to A. This argues for at least considering mixed signature for the capability metric.

---

## Stage 6: Signature for ShaperOS

### Motivation

ShaperOS has multiple subsystems, each with potentially different signature requirements. This stage works through concrete scenarios to determine which subsystems can share a signature and which need their own, with mediating maps between them.

### Exercise 6.1: Capability Intersection

**Scenario:** An agent has three capabilities (read, write, execute) checking access to a resource in Gr(2,4).

**Signature requirement analysis:**

The Plücker embedding maps Gr(k,n) into grade-k blades of Cl(n,0,0). For Gr(2,4), this is Cl(4,0,0). The basis 2-blades are e₁₂, e₁₃, e₁₄, e₂₃, e₂₄, e₃₄ — six of them, matching the dimension of P(∧²ℝ⁴) = P⁵ (RP⁵).

**Check:** Does the meet operation work in Cl(4,0,0)?

The meet of two blades A and B: A ∨ B = ⋆(⋆A ∧ ⋆B).

In Cl(4,0,0), I = e₁₂₃₄. I² = (−1)^(4·3/2 + 0) = (−1)^6 = +1. Good — the Hodge star is well-defined and is an involution.

⋆A = AI⁻¹ = AI (since I² = +1, I⁻¹ = I).

**Verdict:** Cl(n,0,0) works for capability intersection. Pure positive signature. The meet is well-defined because the pseudoscalar is invertible.

**Exercise:** Verify explicitly that for Gr(2,4) in Cl(4,0,0), the meet of two general 2-blades gives the correct intersection dimension.

Take A = e₁₂ (the 2-plane spanned by e₁, e₂) and B = e₃₄ (the 2-plane spanned by e₃, e₄).

```
⋆A = e₁₂ · e₁₂₃₄ = e₁₂₃₄ (need to be careful with signs)
```

Actually, ⋆A = A ⌋ I⁻¹. Let me compute properly.

For the right complement (undual), ⋆e₁₂ in Cl(4,0,0):

⋆e₁₂ = e₁₂ I = e₁₂ e₁₂₃₄ = e₁₂₁₂₃₄

Simplify: e₁(e₂e₁)e₂₃₄ = −e₁₁ e₂₂₃₄ = −1·e₂₂₃₄ = −e₂₂ e₃₄ = −e₃₄.

So ⋆e₁₂ = −e₃₄.

Similarly ⋆e₃₄ = e₃₄ e₁₂₃₄. Work through: this gives ⋆e₃₄ = −e₁₂.

Now: ⋆A ∧ ⋆B = (−e₃₄) ∧ (−e₁₂) = e₃₄ ∧ e₁₂ = e₃₄₁₂ = e₁₂₃₄ (up to sign).

Then ⋆(⋆A ∧ ⋆B) = ⋆e₁₂₃₄ = e₁₂₃₄ · e₁₂₃₄ = I² = 1 (a scalar).

**Interpretation:** A ∨ B = 1 (scalar, grade 0). The meet of e₁₂ and e₃₄ is 0-dimensional — these two planes intersect only at the origin. This is correct: span(e₁,e₂) ∩ span(e₃,e₄) = {0} in ℝ⁴.

Now try A = e₁₂ and B = e₂₃ (overlapping planes):

⋆e₂₃ = e₂₃ e₁₂₃₄. Compute: e₂₃₁₂₃₄ = e₂₃₁₂₃₄. Rearrange systematically:
e₂(e₃e₁)e₂₃₄ = −e₂₁ e₃₂₃₄ = +e₁₂ e₃₂₃₄ = e₁₂ · (−e₂₃₃₄) = e₁₂ · (−e₂ · 1 · e₄) hmm...

Let me just compute the sign by counting transpositions. e₂₃₁₂₃₄: sort to e₁₂₂₃₃₄.

e₂₃₁₂₃₄ → e₂₁₃₂₃₄ (swap 3,1: −1) → e₁₂₃₂₃₄ (swap 2,1: −1, net +1) → e₁₂₂₃₃₄ (swap 3,2: −1, net −1).

e₁₂₂₃₃₄ = e₁ · (e₂²) · (e₃²) · e₄ = e₁ · 1 · 1 · e₄ = e₁₄.

With the sign: ⋆e₂₃ = −e₁₄.

⋆A ∧ ⋆B = (−e₃₄) ∧ (−e₁₄) = e₃₄ ∧ e₁₄. But e₃₄ ∧ e₁₄ = e₃₄₁₄ = 0 because the index 4 is repeated!

So ⋆A ∧ ⋆B = 0, which means A ∨ B... hmm, we need to be more careful. The meet being zero in this formulation means the two subspaces together span the whole space (they're not in "general position" for the meet to be nontrivial at the level of the full algebra). But geometrically, span(e₁,e₂) ∩ span(e₂,e₃) = span(e₂), which is 1-dimensional.

**The issue:** The naive formula A ∨ B = ⋆(⋆A ∧ ⋆B) works when the subspaces are in complementary position. For general position, you need the more careful regressive product definition. This is discussed in Dorst/Fontijne/Mann and in the `amari-enumerative` corrections doc.

**Key takeaway for ShaperOS:** Cl(n,0,0) is correct for the Plücker embedding and basic meets, but the regressive product implementation needs care for non-generic configurations — which is exactly what the CSM class correction handles at the level of intersection numbers.

### Exercise 6.2: Agent Belief States

**Scenario:** An agent maintains a belief state that evolves over time. The belief includes:
- Spatial estimates (where things are) — positive definite
- Temporal ordering (what happened before what) — needs causal structure
- Uncertainty (how confident the agent is) — scalar, always positive

**Signature analysis:**

Spatial estimates: 3D Euclidean → three positive dimensions.

Temporal ordering: Causal structure requires distinguishing "future" from "past" from "spacelike." This is the Minkowski structure: one timelike dimension with opposite sign from space.

Uncertainty: A scalar. Scalars are grade-0 and don't affect the signature.

**Candidate:** Cl(3,1,0) for the belief state. Time is the negative dimension.

**But wait:** The belief state isn't physical spacetime. An agent's "temporal ordering" might be better modeled by a *partial order* (events A and B might be incomparable, like concurrent processes). A partial order isn't a metric structure — it's an order structure.

**Alternative:** Use the degenerate dimension for the "incomparable" direction. Cl(3,1,1): three spatial, one temporal, one degenerate for "unknown ordering." An event with zero component along the degenerate dimension has definite temporal ordering; nonzero degenerate component means temporal ordering is uncertain.

**Exercise:** Work through a specific scenario. Agent observes events A (at time t=1, position x=0), B (at time t=2, position x=3), and C (at unknown time, position x=1). Embed these in Cl(3,1,1) and Cl(3,1,0). In which algebra can you algebraically distinguish "C's temporal position is unknown" from "C is at t=0"?

In Cl(3,1,0), you'd have to assign C some temporal coordinate — say 0. But then C appears to have a definite temporal relationship with A and B, which is wrong.

In Cl(3,1,1), C = e₁ + e₅ (position x=1, degenerate component indicates temporal uncertainty). The degenerate component squares to 0, so C is "partially null" — it has no definite temporal inner product with A or B.

### Exercise 6.3: Memory Grades and Signature

**Scenario:** ShaperOS memory is organized by grade:

| Grade | Interpretation |
|-------|---------------|
| 0 | Raw scalars (activations) |
| 1 | Vectors (features, embeddings) |
| 2 | Bivectors (relations, correlations) |
| 3+ | Higher structure (contexts) |

**Question:** Does the memory model impose signature constraints?

**Analysis:**

Memory *consolidation* lifts patterns from grade-2 (episodic: "A and B were correlated") to grade-3+ (semantic: "A, B, and C form a context"). This is the outer product: if R₁ = a ∧ b (a grade-2 episodic memory) and c is a new observation, consolidation produces R₁ ∧ c = a ∧ b ∧ c (grade-3 semantic memory).

The outer product doesn't depend on signature — a ∧ b is defined the same way regardless of what eᵢ² equals. So consolidation works in any signature.

Memory *recall* uses the inner product (grade reduction): querying grade-3 memory with a grade-1 key gives a grade-2 result (context → relevant relations). The inner product *does* depend on signature.

**The constraint:** If you want memory recall to be "stable" (querying with the same key always gives the same result), you need the inner product to be non-degenerate on the memory subspace. This rules out degenerate dimensions for the "active" memory directions. But degenerate dimensions could represent "archived" or "forgotten" memories — null subspaces where inner products vanish, meaning these memories can't be recalled by any key.

**Verdict:** The memory model suggests a partially degenerate signature: Cl(p,q,r) where r represents the "forgetting dimension." Active memories live in the Cl(p,q,0) subspace; archived memories have nonzero components in the degenerate directions and are unreachable by inner-product recall.

### Exercise 6.4: The Full ShaperOS Signature Map

**Synthesis exercise:** Fill in the signature requirements for each ShaperOS subsystem, then determine which can share a single algebra and which need separate algebras with mediating maps.

| Subsystem | Primary Operations | Signature Requirement | Justification |
|-----------|-------------------|----------------------|---------------|
| Capability checking | Meet, Plücker embedding | Cl(n,0,0) | Positive definite for Grassmannian, invertible pseudoscalar for meet |
| Agent belief (spatial) | Rotations, translations | Cl(3,0,1) | PGA: Euclidean motions as versors, degenerate for ideal points |
| Agent belief (causal) | Temporal ordering, boosts | Cl(3,1,0) or Cl(1,3,0) | Minkowski for causal structure |
| Memory | Inner product (recall), outer product (consolidation) | Cl(p,0,r) | Positive for active dims, degenerate for forgotten |
| Holographic memory | Fourier transform on algebra | Depends on I² | Need I² = −1 for Fourier to be periodic |
| GP transport | Serialization only | None (signature is metadata) | Transmitted in message header |
| Tropical layer | Valuation, min-plus | N/A (tropical semiring) | No Clifford algebra — operates on coefficients only |

**Observations:**

1. Capability checking (Cl(n,0,0)) and spatial belief (Cl(3,0,1)) have different signatures even for the same n. They need separate algebra instances. The mediating map is: drop the degenerate dimension to go from PGA to Euclidean, or add one to go the other way.

2. Causal belief (Cl(3,1,0)) and spatial belief (Cl(3,0,1)) are *incompatible* — one has a negative dimension where the other has a degenerate one. No simple embedding connects them. The mediating map must go through a shared Euclidean subspace.

3. Memory and capabilities can potentially share a signature if the memory dimension matches the Grassmannian dimension. This is a design choice: should Amari's capability algebra and memory algebra be the same?

4. Holographic memory wants I² = −1 (for the Fourier transform to be an involution). From Exercise 1.2: I² = (−1)^(n(n-1)/2 + q). For n=4 (4D algebra), need n(n-1)/2 + q = 6 + q odd, so q must be odd. Cl(4,0,0) gives I² = +1 (wrong). Cl(3,1,0) gives I² = −1 (correct). So holographic memory's signature requirement is compatible with the causal belief system, not the capability system.

**Final exercise:** Draw the "signature map" of ShaperOS as a graph. Nodes are subsystems with their signatures. Edges are mediating maps (embedding, projection, or re-signing) with their mathematical operation. Identify which edges require lossy conversion (information loss) and which are lossless.

---

## Meta-Exercises (Ongoing)

### M1: Signature Journal

For each new domain/paper/module you encounter, record:

```
Date:
Domain:
First-instinct signature:
Analyzed signature:
Match? (Y/N)
If N, why was my instinct wrong?
```

Review monthly. Track your calibration rate.

### M2: Signature Challenge

Pick a random application area (cryptography, fluid dynamics, robotics, economics, music theory) and determine what Clifford algebra signature, if any, would be natural for it. Justify with specific geometric operations the domain needs.

Some starters:
- **Robotics (rigid body motion):** Cl(3,0,1) — PGA. Translations and rotations as versors. Same as spatial belief in ShaperOS.
- **Music theory (pitch class sets):** Cl(0,0,12)? Twelve pitch classes, no natural metric — maybe pure exterior algebra. But interval quality (consonance/dissonance) suggests a metric, possibly Cl(12,0,0) with the inner product encoding harmonic distance.
- **Circuit analysis:** Cl(0,1,0) ≅ ℂ. Impedance is a complex number. But with multiple coupled circuits, you might want Cl(0,n,0) where n is the number of independent modes.
- **Phylogenetics (evolutionary trees):** Tree structure suggests a non-Euclidean metric (hyperbolic geometry). Cl(n,1,0) with the negative dimension giving hyperbolic structure. The Poincaré disk model sits inside Cl(2,1,0).

### M3: "What Breaks" Drill

Take any working GA computation and change one sign in the signature. Predict what breaks, then verify. This is the negative-space version of the exercises above: instead of building the right signature, you're testing your understanding of *why* it's right by seeing exactly how wrong signatures fail.

---

## Appendix: Quick Reference

### Signature Decision Tree

```
Start with your domain's geometric operations:

1. Do you need rotations?
   → At least 2 positive dimensions (or 2 negative: same rotation group)

2. Do you need hyperbolic geometry / boosts / causal structure?
   → Mixed signature: at least one positive AND one negative

3. Do you need points at infinity / projective structure / translations as versors?
   → At least one degenerate dimension

4. Do you need circles/spheres as first-class objects?
   → Conformal embedding: add one positive + one negative beyond the base space

5. Do you need the Hodge star to be an involution?
   → Need I² = +1, i.e., n(n-1)/2 + q is even

6. Do you need the Hodge star to give Fourier-like behavior?
   → Need I² = −1, i.e., n(n-1)/2 + q is odd

7. Do you need all vectors invertible?
   → Avoid degenerate dimensions; either all positive or all negative

8. Do you need null vectors / light cones?
   → Mixed signature (p > 0 and q > 0)
```

### The Periodicity Table

Clifford algebras are periodic mod 8 (Bott periodicity). The isomorphism type of Cl(p,q,0) depends only on p − q mod 8:

| p − q mod 8 | Cl(p,q,0) ≅ |
|-------------|-------------|
| 0 | M(2^(n/2), ℝ) |
| 1 | M(2^((n-1)/2), ℂ) |
| 2 | M(2^((n-2)/2), ℍ) |
| 3 | M(2^((n-3)/2), ℍ) ⊕ M(2^((n-3)/2), ℍ) |
| 4 | M(2^((n-2)/2), ℍ) |
| 5 | M(2^((n-1)/2), ℂ) |
| 6 | M(2^(n/2), ℝ) |
| 7 | M(2^((n-1)/2), ℝ) ⊕ M(2^((n-1)/2), ℝ) |

(n = p + q throughout; M(k, F) = k×k matrices over F)

This means Cl(5,0,0) ≅ Cl(4,1,0) ≅ Cl(3,2,0) (all have p − q ≡ 5 mod 8). They're isomorphic as *algebras* but have different *geometric interpretations* because the inner product structure differs.

**For signature intuition:** Two algebras with the same p − q mod 8 have the same abstract structure (same matrix size over same field). The *geometry* differs. This is why you can't choose signature purely from algebraic considerations — you need the geometric interpretation.

### Recommended Reading Order (Returning to Hestenes)

1. **Chapter 2** (Rotations and Reflections): Read with signature awareness. Every "reflection" is v ↦ −nvn⁻¹ where n is the mirror normal. What happens when n is null?
2. **Chapter 4** (Central Force Problem): The Runge-Lenz vector. Notice Hestenes works in Cl(3,0,0) throughout. Ask: would the Kepler problem look different in Cl(2,1,0)?
3. **Chapter 5** (Rigid Body Motion): The inertia tensor as a linear function on bivectors. This is where the connection to Cl(3,0,1) (PGA) would appear if Hestenes had used it.
4. After Hestenes, read **Dorst/Fontijne/Mann** Chapter 13 (Conformal Model) for Stage 3 material, and **Doran/Lasenby** Chapters 1-4 for Stage 4 (spacetime algebra with the opposite convention from Hestenes).
