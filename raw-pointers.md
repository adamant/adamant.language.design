# Raw Pointers

## Syntax

While C/C++ have well established pointer syntax and Adamant is in that linage, it uses pointers much more rarely. Given that, it made sense to change the pointer syntax for purposes of clarity and freeing up symbols. In terms of clarity, being able to combine the dereference operator in a postfix position with the member access operator seemed useful. In terms of freeing up symbols, the unary star operator and unary ampersand operators aren't actually that useful for anything else, but not overloading their meaning reduces cognitive load.

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

In the initial designs, pointers were allowed to be null, like default pointers in other languages. However, this led to needing some other inconsistent syntax for non-null pointers. Furthermore, if making reference types non-null by default makes sense, why wouldn't it make sense to make pointer types non-null by default? That is why pointers are now non-null and must be made nullable using optional types.

## Valid Pointer Types

At first it was assumed it would be reasonable to have pointers to reference types. Eventually it was realized there was serious issues with this. As a result, only pointers to struct types are allow. This follows the precedent set by the C# language. Problems that would be caused by allow pointers to reference types include:

* References are "fat" they contain both a pointer to the data and a pointer to the vtable. To support calling methods on pointers to reference types, some pointers would have to be fat while other's weren't this would lead to confusion and issues with interop.
* Pointer arithmetic doesn't make sense on pointers to reference types. Pointer arithmetic only makes sense when there is a contiguous sequence of values of the same exact type. They can't be different sizes or different subclasses that need different vtables.
* How to declare a pointer to a reference? If `@Foo` is a pointer to a `Foo`, what is a pointer to a reference to `Foo`? Something like `@ ref Foo` could work but seems awkward and confusing.
* Constructing pointer types from generics leads to confusion. Given a generic type `T`, if `T` is a struct then `@T` is a pointer to it, but if `T` is a class then `@T` is now a pointer to the data of the class, not a pointer to the reference. This is inconsisent and breaks the idea that references are effectively structs that refer to an object.
