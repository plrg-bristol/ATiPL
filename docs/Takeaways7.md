# Takeaways for Week Seven
(Week six was reading week, so no takeaways)

Call-by-name, Call-by-value, and Effects
* KNOW that so far in the course, as specified by the substitution lemma, we have been using a call-by-name (CBN) evaluation strategy
* KNOW that call-by-name (CBN) means that variables stand for terms (as opposed to values as we will see in call-by-value)
* BE ABLE TO execute a simple example using call-by-name e.g.:
  - `f(1 + 1) = (1 + 1) + (1 + 1) = 2 + (1 + 1) = 2 + 2 = 4` (eval happens last)
* KNOW that call-by-value (CBV) means that variables stand for values, in other words, expressions must be evaluated before they are substituted
* BE ABLE TO execute a simple example using call-by-name e.g.:
  - `f(1 + 1) = f(2) = 2 + 2 = 4` (eval happens first)
* UNDERSTAND the difference between CBN and CBV
* KNOW that evaluation order does not change **pure** results
* KNOW that the difference only becomes noticeable in the presence of **effects** (assuming you have no way of noticing number of eval steps)
* KNOW that CBN is strongly related to lazy evaluation in purely functional languages (and Haskell uses the "call-by-need" optimised variant)
* KNOW that CBV is what is used by almost all languages with effects (C, Java, Scala, JS, OCaml, Scheme, etc.)

The call-by-value λ-calculus
* KNOW that the call-by-value λ-calculus is a version of the STLC in which all substitutions replace a variable with a value.
* UNDERSTAND that changing evaluation order does not effect the statics of language
* UNDERSTAND that only dynamic constructs that involve substitution need be changed to achieve this variant
* BE ABLE TO adjust the dynamics of a call-by-name language to be call-by-value (add val constraints on value judgements and constructs that involve substitution)
* BE ABLE TO prove progress and preservation for the call-by-value λ-calculus

Effects
* UNDERSTAND that the difference only becomes noticeable in the presence of **effects**
* UNDERSTAND the adjustments that need to be made to statics and dynamics to introduce a printing effect
* BE ABLE TO introduce a printing effect to a language
* KNOW
  - CBN and CBV produce the same output
  - CBN and CBV differ in eval steps
  - CBN and CBV differ in presence of effects
* BE ABLE TO give an example showing these differences between the evaluation strategies

---
Key:

KNOW = a fact that you have memorised / written down in a place you can find it again

UNDERSTAND = something you can explain to another, where you don't just know what, but why and how

BE ABLE TO = something you can replicate again on your own and without guidance
