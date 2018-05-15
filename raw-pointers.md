# Raw Pointers

While C/C++ have well established pointer syntax and Adamant is in that linage, it uses pointers much more rarely. Given that, it made sense to change the pointer syntax for purposes of clarity and freeing up symbols. In terms of clarity, being able to combine the dereference operator in a postfix position with the member access operator seemed useful. In terms of freeing up symbols, the unary star operator and unary ampersand operators aren't actually that useful for anything else, but not overloading their meaning reduces cognative load.

A number of possible syntaxes were considered. They were:

| Syntax          | Address Of  | Dereference | Member   | Mutable Pointer | Immutable Pointer |
| --------------- | ----------- | ----------- | -------- | --------------- | ----------------- |
| C/C++           | `&x`        | `*x`        | `x->y`   | `*mut T`        | `*T`              |
| `@` Address†    | `@x`        | `^x`        | `x^.y`   | `@mut T`        | `@T`              |
| `@` At          | `&x`        | `@x`        | `(@x).y` | `&mut T`        | `&T`              |
| ptr             | `ptr.to(x)` | ?           | `x.y`    | `ptr<mut T>`    | `ptr<T>`          |

† Dereference matching type declaration. Thus type is pointer to `T` and matches expression pointer to `x`. Or use "address of" instead of "pointer to". This matches a example from JAI.

The `@` meaning "at" syntax is confusing to programmers familiar with C++ reference syntax. Also, it doesn't provide a clean member access unless the dot operator auto-dereferences which I've never liked.

The `ptr` type seemed a good idea because it demotes pointers from a first class language feature. However, it has some problems. The `ptr` type overloads the dot operator. This is consistent with the behavior of the dot with variable references. There doesn't seem to be a good way to handle dereference here though. Perhaps there is some operator that could be allowed to be overloaded. That operator maybe should be allowed on variable reference types to get the underlying reference.

In the intial designs, pointers were allowed to be null, like default pointers in other languages. However, this led to needing some other inconsistant syntax for non-null pointers. Furthermore, if making reference types non-null by default makes sense, why wouldn't it make sense to make pointer types non-null by default? That is why pointers are now non-null and must be made nullable using optional types.
