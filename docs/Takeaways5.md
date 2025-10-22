# Takeaways for Week Five

Termination for the simply-typed λ-calculus
* KNOW that the STLC terminates
* KNOW the formal statement of termination: For every ⊢ e : τ there exists a v val such that e -->∗ v.
* UNDERSTAND that fulfilling this property is rare
* I DO NOT expect you to know the proof here (https://www.cs.cmu.edu/~rwh/courses/chtt/pdfs/kripke.pdf), this paper is intended as enrichment

Recursion and fixed points
* KNOW that a recursive function is one that calls itself
* UNDERSTAND that the introduction of general recursion violates the termination property, because it is up to the user to ensure that their programs terminate (that they only recurse on smaller values, working towards a base case)
* UNDERSTAND the mechanics of recursion without Haskell's syntax, where instead of simply calling the function you are defining by name in the definition, we abstract out the recursive call and find the fixed point as demonstrated by the fix function:

```haskell
fix :: (a -> a) -> a
fix f = f (fix f)

h :: (Integer -> Integer) -> (Integer -> Integer)
h f n = if n==0 then 1 else n * (f (n-1))

fact :: Integer -> Integer
fact = fix h
```

PCF
* KNOW that PCF (Programming Computable Functions) = (some version of) the STLC + fixed points
* KNOW that PCF's functions are partial, meaning that the may not be defined for all inputs
* UNDERSTAND PCF's syntax chart
* UNDERSTAND PCF's statics, in particular that of the Fix construct
* UNDERSTAND PCF's dynamics, in particular that of the Fix construct
* (you will be given PCF's statics and dynamics in the exam)
* BE ABLE TO write a well-typed PCF term using these statics
* BE ABLE TO evaluate a PCF term using these dynamics

Programming in PCF
* BE ABLE TO write programs in PCF (a helpful technique is to write it in haskell, then convert it)

Turing-completeness
* UNDERSTAND what partial functions are PCF definable
* KNOW that PCF is Turing-Complete
* (The details of Turing-Completeness with relation to the partial recursive functions and the Church-Turning thesis are just there for your interest)

Sequentiality
* UNDERSTAND that PCF is inherently sequential, and cannot compute even the simple parallel or function

---
Key:

KNOW = a fact that you have memorised / written down in a place you can find it again

UNDERSTAND = something you can explain to another, where you don't just know what, but why and how

BE ABLE TO = something you can replicate again on your own and without guidance
