# Takeaways for Sam Week Four

KNOW that this week, we will expand our little lang to the simply-typed λ-calculus (STLC).
KNOW this consists of adding sum and product types (which correspond to Either and pairs from Haskell), and exponential types (functions) to the little lang.

Products
* KNOW product types correspond to tuples
* KNOW that binary products (pairs) allow us to write functions that return two values
* KNOW that the nullary product (unit) allows us to write functions that return nothing
* KNOW that the syntax for product types normally uses x and 1 (echoing the notation for the multiplicative monoid)
* KNOW that statics can be split up into introduction and elimination rules where:
  - introduction rules create an instance of a type
  - elimination rules remove / project from an instance of a type
* KNOW that syntax for products normally involves brackets for introduction and pies for projection
* BE ABLE TO expand the statics and dynamics of our little language to include appropriate rules for products
* BE ABLE TO write a syntactically correct and well-typed term including products, justifying its correctness with a typing derivation in the appropriate context
* BE ABLE TO use the dynamics of products to evaluate a term including them
* BE ABLE TO expand the definitions of substitution, inversion, and canonical forms to include products

Sums
* KNOW sum types correspond to choices between values
* KNOW that binary sums (pairs) allow us to write programs that pattern match
* KNOW that the empty type (void) corresponds to no choice
* KNOW that the syntax for sum types normally uses = and 0 (echoing the notation for the additive monoid)
* KNOW that syntax for sums normally involves inL and inR constructors for introduction, and a case statement for elimination
* BE ABLE TO expand the statics and dynamics of our little language to include appropriate rules for sums
* BE ABLE TO write a syntactically correct and well-typed term including sums, justifying its correctness with a typing derivation in the appropriate context
* BE ABLE TO use the dynamics of sums to evaluate a term including them
* BE ABLE TO expand the definitions of substitution, inversion, and canonical forms to include sums

Functions - Statics
* KNOW that the syntax for function types typically uses ->
* KNOW that the syntax for functions normally uses a lambda
* KNOW the standard typing rules for Lam and App (note that lam can slightly differ depending on whether or not we type the argument)

Functions - Dynamics
* KNOW that functions are discharged via _beta-reduction_
* UNDERSTAND how the dynamics control the evaluation order of functions in our language: that lambda expressions are values, because in our eval order, we work on the function expression, until it is ready to apply, until it is a lambda expression, then and only then can we apply it using beta reduction
* BE ABLE TO use the dynamics of functions to evaluate a term including them

Functions - Examples
* KNOW that our formulation of function supports _higher-order_ functions
* KNOW Higher Order (HO) Functions are functions that take other functions as parameters.
* BE ABLE TO write a term using functions, including justification via typing derivation
* BE ABLE TO write a HO function in this language, justifying its well-typed-ness with a derivation

Properties
  * KNOW the simply-typed λ-calculus (STLC) = product types + sum types + function types (+ constants)
  * **BE ABLE TO prove type safety for the STLC**

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
