# Takeaways for Week Three

Technically in last week's lecture notes, but I only want you to have taken this away this week:
  * KNOW that the way we have specified the dynamics of our program is called _operational semantics_ that are executed by an _abstract machine_ (there are others, the main one being _denotational semantics_, which you won't learn in this unit, but I think it is easier as its similar to haskell )

Values
  * KNOW a simplistic way of looking at a computer program is that it computes a value, and for now, we will design our dynamics around that goal
  * UNDERSTAND the judgements VAL-NUM and VAL-STR state that the terms num[n] and str[s] are trivially values, and that they are the only values in our language so far (a la prop 1 in the lecture notes)
  * UNDERSTAND that values are closed terms
  * BE ABLE TO read the Values section of the dynamics lecture notes and without much effort / time conclude the above takeaways aka that the section just makes sense. I've put this check, because given everything you've learnt so far, you should be able to understand a new judgement with its rules and a few describing words (that's what you'll encounter in academic papers)

Transitions
  * KNOW that the dynamics of a language (how it evaluates to a value) can be specified by transition rules
  * KNOW that terms can be thought of as states of a transition system that runs programs of our language
  * KNOW that the --> judgement defines a relation that species how to step through a program
  * KNOW that there are different classes of transition rules:
    - _instruction transitions_, which perform computation
    - _search transitions_, which determine the order of evaluation of the language
  * Rules for transitions:
    - BE ABLE TO interpret transition rules i.e. use the rules to evaluate a term, justifying each step with a derivation
    - BE ABLE TO use transition rules to express the dynamics for a language of your design
  * KNOW the convention for writing a specific transition is to highlight the bit that changes

Multi-step transitions
  * KNOW a series of valid transitions is called a _transition sequence_
  * KNOW a _reflexive relation_ is one where every element is related to itself (in this context, you can think of this as representing taking no steps in a transition sequence, possibly ending a sequence)
  * KNOW a _transitive relation_ is one where relations can be chained together (in this context, you can think of this as adding a single step the transition sequence)
  * UNDERSTAND that the _reflexive transitive closure_ of a transition system species how to create a transition sequence (take multiple steps), and can be defined by adding two rules (one that represents the zero step, and one that represents adding another step), and is generally denoted by adding a * to the transition symbol e.g -->*
  * BE ABLE TO specify the _reflexive transitive closure_ of a given transition system

Basic properties
  * KNOW if values are the goal of our transition system, they are the final states i.e. there are not transitions after we hit a value
  * UNDERSTAND that the Finality proposition states the above notion
  * UNDERSTAND that the dynamics we have defined strictly determine evaluation order, there is only one transition that can be taken for any given term
  * UNDERSTAND that the Determinism proposition states this above notion
  * KNOW that e⇓v means that e -->∗ v ∧ v val

Type Safety
  * KNOW that type safety means that well-typed and closed expressions do not go wrong and can be broken down into _progress_ and _preservation_
  * KNOW that _preservation_ (the safety property) says that the type of a term is preserved under evaluation
  * KNOW that _progress_ (the liveness property) says that if we are not done evaluating (if we have not hit a value), we can and will continue evaluating i.e. there will always be an available transition (unless we are done)

**Preservation**
  * KNOW (Preservation). If ⊢ e : τ and e --> e' then ⊢ e' : τ .
  * BE ABLE TO prove preservation (by induction) for a given language
  * KNOW that the inversion and substitution lemmata will be invaluable in such proofs

**Progress**
  * BE ABLE TO state the canonical forms lemma for a given set of rules
  - KNOW that canonical forms lemma can be proven by "inspection" (‘look at the rules, there can’t be another way!’)
  * KNOW (Progress). If ⊢ e : τ then either e val or e --> e' for some e'
  * BE ABLE TO prove progress (by induction) for a given language
  * KNOW that the canonical forms lemma will be invaluable in such a proof

**PROGRESS AND PRESERVATION (Type Safety) ARE THE KEY THEOREMS OF THIS UNIT!!!**
From here onwards, we will add new features to our language, and ensure it remains well behaved by proving type safety. **Make sure you understand them and can prove them.**
You will (or should) see them in PL papers that define new languages

---
Key:

KNOW = a fact that you have memorised / written down in a place you can find it again

UNDERSTAND = something you can explain to another, where you don't just know what, but why and how

BE ABLE TO = something you can replicate again on your own and without guidance
