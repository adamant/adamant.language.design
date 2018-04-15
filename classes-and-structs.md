# Classes and Structs

## Value Types

The `struct` keyword is used to define value types. Originally, Adamant was not going to have value types, but only reference types declared with `class`. This ran into several issues.

First, it was unclear how to interop types with C without complicated marshalling since all types could have a vtable. There were also issues about subtyping since any type could be subclassed. How would one handle a subclass of `int` being passed to an external function? Still it would have been possible to apply the `external` keyword to class declarations and restrict external classes to have no base class and no subclasses.

Second, there were problems around combining move and copy semantics into reference types. For example, consider a reference to a `var` containing a class with move semantics. What if one were to assign a different instance into it that was actually a subclass. Since they would be different sizes, that could never be implemented unless types with move semantics were still stored as references to the heap. Of course, the compiler could probably optimize that away in many cases, but it seemed foolish to rely on that so much.

Third, in implementing low level functionality like reference counting it seemed really useful to have a type that could be certain to exist on the stack as a value type.

## New Operator

Any value with mutable state should be created with the `new` operator. Rust doesn't have a new operator. However, it was decided that for Adamant the explicitness of having a new operator for allocating memory was good. It then might seem to make sense to not use new for structs. Using new for structs in C# has always felt a little weird. However, the optimizer of Adamant is expected to frequently convert reference types into stack allocations so they might end up equivalent. Also, it make structs consistent. And it would seem weird to declare struct constructors using new but then call them without new. One can't just have static functions build structs because of safety around definite assignment.

## All Methods Must Have a Unique Implementation

Given a method `M` in interface `A` and interfaces `B` and `C` that implement `A` and override `M`, a class `D` that implements `B` and `C` must override `M` to provide a unique implementation of `M` to be called. This applies even if `B` and `C` rename `M`. At first glance this seems a strange restriction to place. However, since Adamant is trying to not lock in an implementation, this restriction ensures certain implementations are possible, and can be safely removed in the future if desired. Specifically, it enables a vtable implementation where every method across all classes is assigned a unique slot and there is only one vtable pointer in an object. If this restriction were not in place, it would then be ambiguous which method pointer to put in the `M` vtable slot for class `D`.

## `internal` Access Modifier

Several other keywords were considered instead of `internal` for that access modifier. The internal keyword doesn't clearly indicate internal to what. For a while `package` was used instead. However, package reads as if one is actually declaring a package. The synonyms of internal `limited` and `restricted` were also considered. They have the same problem of not clearly indicating what unit they are relative to. Given that, it seemed best to stay with `internal` for familiarity to C#.
