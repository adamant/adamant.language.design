# Terminology

## Avoid

The following terms are to be avoided. Typical reasons include ambiguity, multiple uses and programmer confusion.

* "static": The term static means many different things in different contexts, is misused by many languages and its English definition has a weak connection to its meaning in programming. While it could have been profitably used, at this point, it is best avoided entirely.

## Decisions

* "Generics", "Generic Class", "Generic Function", "Generic Parameters", "Generic Arguments": Generics seems to be the correct term for what is being done here. Sometimes these are called "Type Parameters", but in Adamant they may not be types. In some ways, the Adamant model is closer to C++ or D templates. However, the template terminology was avoided because templates are structurally typed carry negative connotations in many people's minds. The term "Generic Parameter" and "Generic Argument" are less than ideal though because their English meaning is not specific enough.
