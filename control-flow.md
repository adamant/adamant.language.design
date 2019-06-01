# Control Flow

## No Python Style Loop Else

Python's loop else condition runs after the loop as long as break was not used. A feature like this was considered, though it would have needed a better keyword. However, that construct is more useful when selecting an item out of a collection, and in Adamant this will *not* be done with the `for` loop. Since `for` loops operate on iterators, using a filter on the iterator is a better and easier way to do this. Also, it wasn't clear how to combine such a feature with the existing loop else feature. If it were added, a keyword sequence like `if not break` might be good.

## Control Flow Requires Blocks not Parenthesis

Control flow like `if`, `for` etc. require block statements and do not have parentheses around the expression just like in Rust. Originally, control flow was C style where the expression portion must be surrounded with parentheses, but the statement can be any statement. The current approach solves the dangling else issue and also makes loop else unambiguous (i.e. people won't think the loop else is for an if). More importantly, I think this makes scopes clearer. Whatever effect scopes have on value lifetimes, they will be visually apparent in the code. With C style control flow, there is a scope introduced, but it may not be visually apparent when it is not surrounded by curly braces.

## `loop` Keyword

As in Rust the justification is that the control flow analyzer treats it differently. Also, just makes the thing clearer.

## `=>` Operator

The expression evaluation operator was the result of trying to come up with a syntax for if expressions and after considering many different syntaxes, realizing that this was essentially the same problem as match, and Rust used `=>` for match expressions which I was likely to match just for familiarity.

Before this syntax, the use of a keyword `is` was considered. It was thought of as mirroring the exiting of functions and loops.

| Structure                 | Exit     |
| ------------------------- | -------- |
| Function                  | `return` |
| Loop                      | `break`  |
| Choice (`if` and `match`) | `is`     |

This might have looked like:

```adamant
let x = if cond
        {
            DoSomething();
            is 5;
        }
        else
        {
            SomethingElse();
            is 6;
        };

let y = if cond is "Hello" else is "World";
let z = match v
        {
            [0, y]
            {
                Action();
                is y;
            },
            [x, 0] is x,
            [x, y] is x + y,
        };
```

But using `is` for this was also inconsistent with with C#'s use of `is` for type checking. It seemed prudent to leave the `is` keyword available for that.
