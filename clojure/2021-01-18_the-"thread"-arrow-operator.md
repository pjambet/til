# The "thread" arrow operator

Nothing to do with "Threads" as in the treads in a process, concurrency,
parallelism and all that.

It seems similar to the pipe operator in Elixir, to chain function calls.
Here's a small example:

```clojure
(->
 ["list" "of" "strings"]
 first
 clojure.string/capitalize)
;; => "List"

;; equivalent to:
(clojure.string/capitalize (first ["list" "of" "strings"]))
```

and 

```clojure
(->>
 ["list" "of" "strings"]
 (take 2)
 (map clojure.string/join))
;; => ("list" "of")

;; equivalent to:
(map clojure.string/join (take 2 ["list" "of" "strings"]))
```

Docs:
- https://clojure.org/guides/threading_macros
- https://clojure.github.io/clojure/clojure.core-api.html#clojure.core/-%3E

There are other functions, such as `as->`, which I know nothing about at this point
