# Takeaways for Hoare Logic

KNOW that type safety says well-typed programs do not get stuck, but it cannot tell apart programs of the same type (e.g. doubling, the constant 0 and the nth prime all have type Int → Int)
KNOW that this week we add a third semantics, _axiomatic semantics_, which states what a program _should_ compute, so that we can prove that it does

## Hoare Logic I: Triples and rules

The language: Imp
* KNOW that we move from the λ-calculus to Imp, a minimal imperative language, because Hoare logic reasons about how _state_ changes, and assignment is Imp's state-changer
* KNOW the syntax of Imp: arithmetic expressions `a`, boolean expressions `b`, and commands `skip`, `x := a`, `c ; c`, `if b then c else c`, `while b do c`
* KNOW that a state is a total map from variables to integers, σ : Var → Z, and that σ[x ↦ v] is σ with x remapped to v
* KNOW that **σ changes meaning**: previously it ranged over types, from now on it ranges over states
* KNOW that the dynamics of Imp is _big-step_, ⟨c, σ⟩ ⇓ σ', going straight from a command to its final state
* UNDERSTAND why we use big-step: a specification only constrains the initial and final states, which is exactly the relation ⇓ gives us
* KNOW that big-step and small-step agree: ⟨c, σ⟩ ⇓ σ' iff ⟨c, σ⟩ ↦* ⟨skip, σ'⟩

Triples
* KNOW that an _assertion_ P is a predicate on states (a first-order formula over the program variables), and σ ⊨ P means "P holds in state σ"
* UNDERSTAND that assertions are not Imp boolean expressions: they can use quantifiers, and they are the language of mathematics, not of the program
* KNOW the Hoare triple {P} c {Q}: if P holds before c, **and c terminates**, then Q holds afterwards (P is the _precondition_, Q the _postcondition_)
* KNOW that this is called _partial correctness_, as it says nothing about whether c terminates
* UNDERSTAND why {P} while true do skip {Q} is valid for every P and Q (it never terminates, so the triple is vacuously true)
%* KNOW validity: ⊨ {P} c {Q} iff for all σ, σ', if σ ⊨ P and ⟨c, σ⟩ ⇓ σ' then σ' ⊨ Q
%* BE ABLE TO decide whether simple triples are valid, e.g. {True} x := 5 {x = 5} (yes), {True} x := 5 {x = 6} (no), {x = 6} x := 5 {x = 5} (yes)

The rules
* UNDERSTAND the six rules of Hoare logic: Skip, Assign, Seq,
* UNDERSTAND that five of them are syntax-directed (look at c, apply the rule), but Conseq can be applied anywhere at any time
* UNDERSTAND the assignment axiom {Q[a/x]} x := a {Q}, and that it is read right to left: to guarantee Q after x := a, demand that Q with a in
place of x holds before
* BE ABLE TO apply the assignment axiom to small examples, e.g. to get x > 0 after x := x + 1 you need x > −1 before
* UNDERSTAND that in Seq, the midpoint assertion R is the glue, and that the assignment axiom computes it for us
* UNDERSTAND that in If, each branch may assume the guard and the branches must establish the same Q
* UNDERSTAND the While rule and that I is the _loop invariant_: true on entry, preserved by the body, and hence true on exit, together with ¬b
* UNDERSTAND that Conseq is the seam between program reasoning and logical reasoning: its premises are entailments discharged by ordinary maths or e.g. an SMT solver
* UNDERSTAND the direction of Conseq: strengthen the precondit (you may always assume more and promise less, neverassume less and promise more)


A worked example: the swap
* KNOW that _logical (auxiliary) variables_ such as A and B do not appear in the program, and name initial values so that we can state what the
program should do
* UNDERSTAND that verification is a backward calculation: start from the postcondition and push it up through each assignment
* BE ABLE TO prove similar loop-free examples using Assign, Seq and Conseq

## Hoare Logic II: Invariants and weakest preconditions

Loop invariants
* UNDERSTAND that the While rule does not compute the inou supply, so finding I is the creative act of program verification
* KNOW the three obligations for proving {P} while b do
  - _Establish_: P ⇒ I (I holds on entry)
  - _Preserve_: {I ∧ b} c {I} (the body maintains it)
  - _Conclude_: I ∧ ¬b ⇒ Q (on exit, I gives you Q)
* UNDERSTAND that an invariant is a generalisation of the postcondition that is also inductive: strong enough to give Q at the end, stable
enough to survive a lap
* UNDERSTAND that only "preserve" touches the program; the other two obligations are pure logic
* BE ABLE TO find an invariant by generalising the postcondition, e.g. for summing 0 to n − 1, generalise n to i: I ≡ s = Σ_{k=0}^{i−1} k ∧ i ≤ n

Weakest preconditions
* KNOW that wp(c, Q) is the weakest assertion P such thakest" means most permissive (it demands the least)
* UNDERSTAND that ⊨ {P} c {Q} iff P ⇒ wp(c, Q), so wp turns a verification question into an implication you can hand to a solver
* UNDERSTAND the wp calculus for loop-free code:
  - wp(skip, Q) = Q
  - wp(x := a, Q) = Q[a/x]
  - wp(c1 ; c2, Q) = wp(c1, wp(c2, Q))
  - wp(if b then c1 else c2, Q) = (b ⇒ wp(c1, Q)) ∧ (¬b
* UNDERSTAND that the wp calculus is the rules of Lecture 8 read as an algorithm: purely syntax-directed, right to left
* UNDERSTAND why there is no wp clause for while: it is a fixed point that unfolds to an unbounded disjunction over the number of iterations, which is why we annotate loops with invariants
* KNOW that wp distributes over conjunction, wp(c, Q1 ∧ so a conjunctive specification can be verifiedcomponentwise
* BE ABLE TO compute wp for a loop-free command

Verification conditions
* BE ABLE TO prove a program with a loop (similar to summing 0 to n − 1) by coming up with the loop invariant, generating the VCs and proving them (when they are very simple)

**THE INVARIANT IS THE ONE CREATIVE STEP OF VERIFICATIONION.**

---
Key:

KNOW = a fact that you have memorised / written down in a place you can find it again

UNDERSTAND = something you can explain to another, where you don't just know what, but why and how

BE ABLE TO = something you can replicate again on your own and without guidance
