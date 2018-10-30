# Operators

## Ranges

There were many options for how the range operator syntax. Initially, it was thought it should be inclusive of the start value and exclusive of the end value. This would make the common C for loop case the default. However, it was very difficult to come up with a good syntax for the inclusive case. After looking at Swift and reviewing the [operators used by other languages for range](http://rigaux.org/language-study/syntax-across-languages/VrsDatTps.html#VrsDatTpsRng) this was changed. It appears most languages use `..` to be inclusive of both ends. This then opens up `..<`, `<..` and `<..<` for ranges exclusive of their end values. This syntax was inspired by the Swift `..<` operator for half open ranges. It was decided that C style for loops should now be rare enough that it isn't an issue that they have a longer, more awkward syntax.
