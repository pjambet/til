# A function returning another function

I was reading about Railway Oriented Programming earlier today, and ended up
deciphering a lot of F# code, the following defines a function, that returns
another function, the signature is:

``` fsharp
bind : ('a -> Result<'b,'c>) -> Result<'a,'c> -> Result<'b,'c>
```

``` fsharp
let bind switchFunction =
    fun twoTrackInput ->
        match twoTrackInput with
        | Success s -> switchFunction s
        | Failure f -> Failure f
```

You can also use the automatically curried version, with two paramaters:

``` fsharp
let bind switchFunction twoTrackInput =
    match twoTrackInput with
    | Success s -> switchFunction s
    | Failure f -> Failure f
```
