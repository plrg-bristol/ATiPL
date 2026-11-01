# Takeaways for Separation Logic

KNOW that Hoare logic reasons about variables, which are independent boxes: assigning to x cannot change y
KNOW that this week we add the _heap_, and that assumption stops holding

## Separation Logic I: The heap, the separating conjunction and the frame rule

Why Hoare logic breaks on the heap
* KNOW that [x] means "the heap cell that x points to"
* UNDERSTAND why the assignment axiom fails for heap mutation: {[y] = 3} [x] := 4 {[y] = 3} looks fine, but is wrong when x and y hold the same address
* KNOW that this is _aliasing_: two different names denote one cell, and substitution is syntactic, so it cannot see it
* UNDERSTAND that without a way to say "these cells are separate", a specification must mention the whole heap plus a disequality for every pair of pointers (global reasoning)

The model
* KNOW that a state is now a _store_ s : Var → Val (total, the old σ) and a _heap_ h : Loc ⇀ Val (partial, finite domain dom(h))
* KNOW that we write s, h ⊨ P, and that assertions now describe the _shape_ of the heap
* KNOW the two basic heap assertions:
  - emp: the heap is empty, dom(h) = ∅
  - x ↦ v: the heap is _exactly one cell_, at address x, holding v

The separating conjunction
* UNDERSTAND that s, h ⊨ P ∗ Q iff h splits as h₁ ⊎ h₂ with disjoint domains, s, h₁ ⊨ P and s, h₂ ⊨ Q
* UNDERSTAND that the split is existential: "there is some way to divide the heap so that…"
* UNDERSTAND the difference between ∗ and ∧: x ↦ 3 ∗ y ↦ 3 forces x ≠ y (two cells), while x ↦ 3 ∧ y ↦ 3 allows x = y (one cell)

Small axioms
* UNDERSTAND the four heap commands and their _small axioms_, each stated on its _footprint_ (the smallest heap that makes sense):
  - mutation: {x ↦ _} [x] := a {x ↦ a}
  - lookup: {x ↦ v} y := [x] {y = v ∧ x ↦ v} (y fresh)
  - allocation: {emp} x := new(a) {x ↦ a}
  - disposal: {x ↦ _} dispose(x) {emp}
* UNDERSTAND that each small axiom mentions only the cell the command touches

The frame rule
* UNDERSTAND the frame rule: from {P} c {Q} infer {P ∗ R} c {Q ∗ R}, provided c modifies no variable free in R
* UNDERSTAND what it says: if c works on footprint P, it leaves any disjoint heap R untouched
* UNDERSTAND why the side condition matters: without it, framing x ↦ 3 around x := new(4) gives x ↦ 4 ∗ x ↦ 3, which says x points to two cells
* KNOW that small axioms + the frame rule = _local reasoning_: prove a command once, on its footprint, and reuse it in any larger heap
* BE ABLE TO use the frame rule to lift a small axiom to a larger heap, e.g. {x ↦ 3 ∗ y ↦ 3 ∗ z ↦ 7} [x] := 4 {x ↦ 4 ∗ y ↦ 3 ∗ z ↦ 7}


## Separation Logic II: Inductive predicates

Inductive predicates
* UNDERSTAND why we need them: x ↦ v describes a fixed, finite heap, but a linked list has unboundedly many cells
* KNOW that a cell x ↦ v, z holds a value v and a next-pointer z
* UNDERSTAND the list segment predicate:
  lseg(x, y) ≡ (x = y ∧ emp) ∨ (x ≠ y ∧ ∃v, z. x ↦ v, z ∗ lseg(z, y))
* UNDERSTAND that a full (null-terminated) list is list(x) ≡ lseg(x, nil)
* UNDERSTAND that the ∗ in the recursive case makes the head cell disjoint from the rest: separation is built into the datatype, so a list cannot loop back on itself

Unfold, operate, fold
* KNOW that a predicate is used by _unfolding_ its definition one step at a time
* KNOW the rhythm of every list proof: unfold at the front, operate on the exposed cell, fold back up
* UNDERSTAND that the ∗ guarantees the exposed cell and the tail never alias, so you can mutate the head and frame the tail
* BE ABLE TO prove a small loop-free example, e.g. {listC(i, v·α)} [i.val] := w {listC(i, w·α)} by unfold, mutation framing listC(z, α), fold


**SEPARATION IS THE KEY IDEA: ∗ BUILDS IN DISJOINTNESS, AND THE FRAME RULE TURNS THAT INTO LOCAL REASONING.**

---
Key:

KNOW = a fact that you have memorised / written down in a place you can find it again

UNDERSTAND = something you can explain to another, where you don't just know what, but why and how

BE ABLE TO = something you can replicate again on your own and without guidance
