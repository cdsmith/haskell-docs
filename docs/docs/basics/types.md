
## The type of Booleans

`True` is a value in Haskell. Its *type* is `Bool`. In Haskell, we can state this as:

=== "In a repl"

    ```haskell
    True :: Bool -- (1)!
    ```

    1.  Read "X :: Y" as: "the value X has the type Y"

=== "In a file"

    ```haskell
    example :: Bool
    example = True
    ```

Similarly, 

```haskell
False :: Bool
```

!!! Note
    In Haskell, everything from simple values like `True` to complex programs have a unique type. 

!!! Tip
    Haskell types can be quite complex. To understand a type, always ask: what do the values belonging to this type look like?

## The type of integers

`Int` is a type for integers, as in:

```haskell
5 :: Int
```

??? Gotcha
    `5` can have a more general type in Haskell. See [here](faq/numbers.md)


<!-- Haskell's type system is such an important feature, and so useful for understanding the language, that it is a good place to begin.

Every expression (that includes all programs) in the language has a unique type. -->


## Functions

A function in Haskell means the same as a function in mathematics: it takes an input and produces an output. The type of the function depends on the type of the input and the type of the output. 

=== "In a repl"

    ```haskell
    (\x -> x > 3) :: (Int -> Bool)
    ```

=== "In a file"

    ```haskell
    exampleFunction = (\x -> x > 3) :: (Int -> Bool)
    ```

!!! Note
    In Python, this would be written: `lambda x: x > 3`

We can also define functions without the lambda syntax, like so:

```haskell
exampleFunction :: Int -> Bool
exampleFunction x = x > 3
```

## Product types (tuples)

Pairs of values are themselves values. For example `(True, False)` has type `(Bool, Bool)`:

```haskell
(True, False) :: (Bool, Bool)
```

!!! Note
    `(Bool, Bool)` is a type defined in terms of another type, `Bool`. We could change either the left-hand or right-hand type, to get new types, like:
    
    - `(Bool, Int)`
    - `(Int, Bool)`
    - `((Bool, Int), Bool)`


## Sum types

If you have two types, say `Bool` and `Int`, then you can generate a new type which is their *disjoint union*, called `Either Bool Int`. 

```haskell
(Left True) :: Either Bool Int -- (1)!
(Left False) :: Either Bool Int -- (2)!
(Right 3) :: Either Bool Int
(Right 7) :: Either Bool Int
```

1.  `Left` is a function which takes `True` as an argument. In other languages, this might be written `Left(True)`

2.  `Right` is a function which takes `True` as an argument. In other languages, this might be written `Right(True)`

!!! Note
    `Left` and `Right` are functions. 

    ```haskell
    Left :: Bool -> Either Bool Int --(1)!
    Right :: Int -> Either Bool Int
    ``` 

    1. Actually, the type is more general: `forall a. a -> Either a Int`. See the section on polymorphism.

## Polymorphism

Here is an example of polymorphism, or universal quantification over types:

=== "Quantifiers implicit"

    ```haskell
    swap :: (a, b) -> (b, a)
    swap (x, y) = (y, x)
    ```

=== "Quantifiers written"

    ```haskell
    swap :: forall a b . (a, b) -> (b, a) -- (1)!
    swap (x, y) = (y, x)
    ```

    1. You'll need the extension `ExplicitForAll` to enable this.


Read this type as saying: for **any** type `a`, and **any** type `b`, this function will take a pair of values, one of type `a` on the left,  and one of type `b` on the right, and give back a pair in the other order.

!!! Note
    Types are always uppercase, but a variable ranging over types like `a` and `b` above are always lowercase.


