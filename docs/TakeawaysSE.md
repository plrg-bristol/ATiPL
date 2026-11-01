# Takeaways for Symbolic Execution

KNOW that for four lectures we _proved_ {P} c {Q} for every input
KNOW that symbolic execution changes the goal: _find one input_ that breaks the program

## Two ways to be wrong

Over- vs under-approximation
* KNOW that no analysis can compute exactly the set of reachable states (it is undecidable), so it must choose which way to be wrong
* KNOW _over-approximation_: cover every real run, and maybe some unreal ones (Hoare logic, VCgen)
* KNOW _under-approximation_: include only real runs, and maybe miss some (symbolic execution)
* UNDERSTAND what a result means in each:
  - over: silence _proves_ there is no bug, but an alarm may be false
  - under: an alarm is a _real_ bug, but silence proves nothing


## The mechanism

Symbolic state
* KNOW that the inputs are _symbolic_ values (α, β, …), not numbers
* KNOW the two parts of a symbolic state:
  - the _symbolic store_ σ: each variable ↦ an expression over the inputs
  - the _path condition_ π: what the inputs must satisfy to reach this point
* UNDERSTAND that going forwards computes the strongest postcondition sp, whose assignment rule needs an ∃ for the old value; the symbolic store avoids the ∃ because the old value already has a name (e.g. y ↦ β becomes y ↦ β + 1)

Execution trees
* KNOW that at if b then c₁ else c₂ execution forks: one path with π ∧ b, one with π ∧ ¬b
* KNOW that each leaf of the execution tree is one path, with its store and path condition
* UNDERSTAND the contrast with Hoare's If rule, which merges both branches into one postcondition that may include unreachable states
* UNDERSTAND the cost of forking: n conditionals in sequence can give up to 2ⁿ paths (_path explosion_)
* BE ABLE TO draw the execution tree of a small program and give each leaf's σ and π
* KNOW that a path is _infeasible_ if its path condition is unsatisfiable (e.g. α > 5 ∧ α < 3), and that infeasible paths are pruned
* KNOW the bug query at an assertion Q: is π ∧ ¬Q satisfiable?
* BE ABLE TO write the query for each path, decide whether it is satisfiable, and give a model, e.g. for if x < 0 then y := −x else y := x; assert y > 0 the right path gives α ≥ 0 ∧ α ≤ 0, with model x = 0


## Loops

* KNOW that symbolic execution has no invariant rule: it unrolls the loop k times, forking at the guard each lap
* BE ABLE TO unroll a loop, giving π and σ for each exiting path, e.g. x := n; while x > 0 do x := x − 2; assert x = 0 gives α ≤ 0, 0 < α ≤ 2, 2 < α ≤ 4, …
* UNDERSTAND what unrolling does not tell you: every bug found is real, but about the inputs that need more than k laps it makes no claim at all

---
Key:

KNOW = a fact that you have memorised / written down in a place you can find it again

UNDERSTAND = something you can explain to another, where you don't just know what, but why and how

BE ABLE TO = something you can replicate again on your own and without guidance
