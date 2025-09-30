# Takeaways for Week Two

The phase distinction
  * KNOW that there are two phases of a computer program's life and what they are:
    - static phase: everything that occurs before running the program (compile time) e.g. lexing, parsing, type-checking, static analysis, etc.
    - dynamic phase: everything that happens when a program is actually run (runtime) e.g. final value, side-effects, exceptions, etc.

Typing judgements
  * KNOW the syntax and components of a typing judgement: `Γ |- e : σ`, where
    - Γ = the _context_/_environment_, an unordered list of variable type _bindings_/_assignments_
    - e = the _program_/_expression_ being typed
    - σ = the type of the result of the program
  * KNOW that a binder is a language construct that closes over (binds) variables. e.g. forall/there exists (you will have met in maths), or let/lambda (you will have met in CS)
  * UNDERSTAND the difference between a free and a bound variable
  * KNOW that a closed expression is one with no free variables
  * KNOW that an open expression is one with free vars
  * UNDERSTAND that α-equivalence/α-conversion asserts that the name of the bound variable doesn't matter i.e. that (\x.x) is equivalent to (\y.y)
  * BE ABLE TO tell if a variable is free or bound
  * KNOW the syntax of a context e.g. Γ = x : σ, y : τ
  * KNOW we will only refer to well-typed things as _terms_ i.e. when there exists Γ and σ such that the judgement Γ ⊢ e : σ is evident, and that we will use the terminology _pre-term_ for similarly shaped things that are not necessarily well-typed.

A little language of numbers and strings
  * Syntax:
    - KNOW that AST stands for _Abstract Syntax Tree_
    - KNOW that a _syntax chart_ is a way of specifying the generation of ASTs
    - KNOW that _Backus-Naur form (BNF)_ a specific type of syntax chart
    - KNOW the different parts of BNF:
      * syntactic category = a group/category/type of syntax e.g. type τ, expression e, etc.
      * abstract syntax = defines how expressions of the language should be written
      * concrete syntax = a user-friendly abbreviation for the abstract syntax
      * recursive calls = mentions of subscripted syntactic categories to the right of the ::= which allow the generation of more complex terms
    - KNOW that Σ normally stands for a some alphabet e.g. our alphabet Σ = {a,b,c...z}
    - KNOW that Σ* represents words of that alphabet, specifically zero or more occurrences of the alphabet strung together e.g. "" ∈ Σ* and "hello" ∈ Σ*, where Σ = {a,b,c...z}
    - BE ABLE TO interpret a syntax chart expressed in BNF notation i.e. you should be able to recognise and produce syntactically correct terms specified by that BNF, and write them as ASTs
    - BE ABLE TO write your own BNF to express the syntax of a language fo your design
  * Rules for typing judgements:
    - BE ABLE TO interpret typing rules i.e. write a well typed term and prove it to be well typed by producing a derivation using the typing rules.
    - BE ABLE TO use typing rules to express well-typedness for a language of your design (we will learn later how to ensure these rules are "good" typing rules, this is just about understanding how to use them to express what is in your head)

Inversion
  - KNOW that _Inversion_ is the formal term for ensuring that rules are "syntax directed". In other words ensuring that they are curated such tha there is only one way of creating each syntactic element e.g. there is only one PLUS rule in our little language, and this ensures that the only way of creating a PLUS is with two expressions of type Num to produce an expression of type Num (never of type Str)
  - UNDERSTAND the importance of curating rules such that Inversion holds (stops programmer doing silly things, which is the whole point of types: to guide the programmer)
  - BE ABLE TO state an Inversion _lemmata_ (plural of lemma) for a given set of typing rules
  - KNOW that inversion can be proven by "inspection" (‘look at the rules, there can’t be another way!’)
  - BE ABLE TO prove Inversion for a given set of rules by inspection and induction (you should be able to write both the informal proof and the formal one)

Weakening
  - KNOW that weakening states: If Γ ⊢ e : τ and x is fresh then Γ, x : σ ⊢ e : τ . (informally this says that adding extra info doesn't change/break things, you will want to know this lemma because it will be a useful tool in later proofs)
  - UNDERSTAND why weakening is a desirable (extra and unrelated information shouldn't change how a program behaves, this is sort of ensuring there are not unexpected side effects of a program)
  - BE ABLE TO prove weakening by induction

Substitution
  - KNOW that substitution is a meta-theoretic operation that describes how variables are instantiated in our programming language (meta-theoretic refers to how this is a concept that exists within the mathematics that we are creating our language in, our meta-language)
  - KNOW that substitution is defined by induction (pattern matching) on pre-terms
  - UNDERSTAND the dangers of variable capture (when a binder mistakenly binds a variable because it happens to share the name - a referential clash)
  - KNOW that α-renaming can avoid variable capture issues
  - KNOW that the Barendregt convention allows us to avoid such issues by assuming that everything has been silently α-renamed in a way that is advantageous for us
  - BE ABLE TO perform a specified substitution
  - **KNOW the substitution lemma states: If Γ ⊢ e : τ and Γ, x : τ ⊢ u : σ, then Γ ⊢ u[e/x] : σ (informally this says that performing substitution will not mess up our types)**
  - BE ABLE TO prove the substitution lemma by induction

---
Key:

KNOW = a fact that you have memorised / written down in a place you can find it again

UNDERSTAND = something you can explain to another, where you don't just know what, but why and how

BE ABLE TO = something you can replicate again on your own and without guidance
