# Principles

There are a number of design principles that are followed throughout Adamant and used as justifications for many design decisions. This section defines those, rather than repeating their definitions below.

## Allow for Future Expansions

Design things in restrictive ways that allow for those restrictions to be lifted in the future if it makes sense. Also, ensure syntax and semantics would be orthogonal to likely future enhancements to the language.

## Be Explicit

Require explicit declaration of things to provide clarity to the reader and a safety check. For example, a class must be declared `abstract` if it has any abstract methods even though the compiler could just implicitly assume the class to be abstract in that case.

## Best Practice Defaults

If there is a clear best practice then that should be the "default" i.e. require no extra keyword or code. For example, the default is that methods are overridable (unlike C++ or Java that require the `virtual` keyword). Another example is the default being immutable and making things mutable requiring the `mut` keyword.

## Do Not Lock in an Implementation

Make design choices that enable as many implementations as possible. We don't want to lock Adamant into a particular approach to implementing the language that may have performance drawbacks.

## Only One Way

Do not provide multiple equivalent ways to do something or express something.

## Support Program Evolution

Code changes over time, the language should make that process as smooth as possible. For example, requiring explicit override or hide keywords allows for a clear handling of the situation where a method is added to a base class that matches a method that was previously present only on a subclass.

## Syntax Matters

Syntax conveys style. For example, the abbreviated keywords of Rust lead to a culture of abbreviated and over shortened names. The Rust community settled on short package names.

Familiar syntax can make it easier to learn the language. Consistent use of syntax for different language features can make things clearer.

## Careful Review

Each feature and syntax should be carefully reviewed to make sure it is in accord with all principles. Need to consider many sources. For example, Kevlin Henny's criticisms of package names based on company names. I would not have thought to re-evaluate that.

Review syntax and semantics across languages. Review reasons for language design. For example, should promises be hot or cold, or promises versus eventual values versus green threads.

## Weirdness Budget

## Be Wary of Untried Features and Syntax

## Orthogonality

## Readability

Code is most limited by readability. A little extra effort in writing the code for greater readability and clarity is worth it.

## Only One Way to Do Things

Versus languages that are opposed to this.
