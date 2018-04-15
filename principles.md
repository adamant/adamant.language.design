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
