---
date: 2021-04-25T01:02
---

# Reading Haskell code

[[[Haskell]]]
[[Heuristics]]


[Learning Haskell](https://www.poberezkin.com/posts/2021-04-21-what-i-wish-somebody-told-me-when-i-was-learning-Haskell.html)

1. Read types first, not code (what, not how)
2. Slow down (it's dense)
3. Don't map to imperative

    > functions are not “called” and “executed”, they are “applied” and “evaluated”.

    > functions do not “return” values, even when they use return > function, they are a binding of function code to the function name.

    > preferring pure over return 5 would both save you typing and help switching mindset.

    > “names” are not “variables”, they are not “assigned”, they are “bound” to values.

    > do syntax does not define execution steps, it defines the sequence of actions bound via their Monad type class interface.

4. Model top down, using types

5. Understand data, class, type and newtype differences

    > Haskell class is a pure interface that can be implemented by many data types. The class does not tell you anything about the data, it only defines supported methods that can be implemented by class instances (another confusing term that does not mean the data instance, it actually means a particular, possibly parameterized type that implements the class).

    > As for the rest, data means “data type”, type means type synonym (just a shorthand for another data type), and newtype means the data type container that allows to differentiate, on a type level, between the data types that have the same internal representation - with zero memory and execution time overhead.
    
7. learn to operate on abstractions regardless of examples

8. Write concisely, functor instead of do
```
    getReversed :: IO String
    getReversed = do
      a <- getLine
      return $ reverse a

    -- same with Functor methods:

    getReversed :: IO String
    getReversed = reverse <$> getLine
```

9. Function evaluation produces no side effects