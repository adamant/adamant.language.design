# Primitive Types

I'm not fond of the name "primitve type". For a while I called them "predefined types". That fit with the fact that some of them are actually defined in libraries. However, primitive type seems to be the standard term and what I found myself calling them anyway.

## Numeric Types

Both Rust and Go use integer values to indicate the bit length of types. However, C# did not and it was already planning for 64 bit architectures.
The numeric sizes were selected based on the following criteria:

1. Anything larger than 64 bit pointers is unlikely any time soon
2. Old 32 bit machines could have 64 bit pointers
3. We want to be friendly to embedded processors that might be special
4. We want standard sizes to be nice
5. Platform dependent sizes cause issues

The default sizes (i.e. those that leave off the bit length) were chosen as a compromise between small enough memory use and enough digits of precision to be useful. Hence 32 bit integers with their more than 9 digits were chosen as the default integer size while 64 bits were chosen for floats and decimals because their 32 bit versions had only 7 digits of precision.

## Optional Type

Different languages use different names for option types (see [Wikipedia Option type: Names and definitions](https://en.wikipedia.org/wiki/Option_type#Names_and_definitions)). At first, the C# convention of referring to them as nullable was followed because it was familiar. It also seemed to make clear that developers should expect that for reference types it would be represented as efficiently as a null pointer. However, the name "nullable" seemed to carry with it too much history and implied that they were bad or dangerous. A more neutral name seemed appropriate. Looking at the options, it seemed that "optional" was the clearest. Both Java and Swift name option types that and they are two of the languages most concerned with clear names. Like Swift the `T?` syntax means it isn't necessary to write out the name optional normally.

When considering what to name the two values of an option type, `Some<T>` and `none`. Seemed the clearly better choice.

## Tuples

Generally, I'm not a fan of tuple types. I feel like their unnamed fields are an anti-pattern leading to confusing code. However, they are frequently used in languages that have them. Probably too frequently used. It wouldn't be hard to create tuples in Adamant by declaring a `Tuple` type overloaded on the number of type parameters or with a `Tuple<Values...>` type. That would certainly be done if they weren't included in the language. Additionally, lists of types are essentially tuple types so it will make working with generics easier. Given that it makes sense to include them in Adamant.

In many other languages tuples have a syntax like `(x,y)` but that seems easily confused with grouping. Also, there is no good syntax for a tuple of one value. Some languages use `(x,)` which just seems ridiculous. Given that the new operator is being used for all values including structs, tuples should be declared as `new (x,y);` and would not be ambiguous (that syntax could be an issue for placement new). However, this would still not be a very distinct syntax for tuples. For example, a new single tuple would be `new (x)` and new empty tuple would be `new ()`. Since Adamant does not have primitive arrays, the square bracket symbols are available for use with tuples. This provides a much more distinct syntax and has precedent in other languages. For example the language [E](https://en.wikipedia.org/wiki/E_(programming_language)) uses them for tuples.

Tuple element access using square brackets could be confusing. For example, `new [x, y][0]`. Also it makes it seem tuples could be accessed with non-constant indexes and would encourage people to declare named constants for tuple indexes. It makes more sense to go with the admittedly ugly Rust style of using integer field names like `t.0` and `t.1`.
