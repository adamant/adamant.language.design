# Naming and Conventions

## Iterators instead of Enumerators

Iterator seems to be the more standard term. It isn't clear that "Enumerable" and "Enumerator" are really clearer.

## Naming Conventions

Originally, the naming conventions were:

* Mutable Class Names, Type Parameters: Mixed_Case_With_Underscores
* Immutable Class Names (including attributes): snake_case
* Namespaces, Functions, Public Fields, Static Variables: PascalCase case
* Parameters, Private & Protected Fields: camelCase

There were a number of issues with this:

* Single word immutable types looked like local variables.
* Associated functions on immutable classes could be hidden by local variables.

  ```adamant
  let lexer = new lexer();
  lexer.StaticFunction(); // error: no method StaticFunction on type `lexer`
  ```

* Fields can act as properties, so it doesn't make sense to give them different casing.
* Properties won't need to be distinguished from their backing fields as often. Use a field instead.
* Changing a type from purely immutable to mutable may not be a breaking change, but would change the naming convention.
* The distinction between mutable and immutable types may not be that important given that immutable is the default and immutable variables of mutable classes are common.

Many possible naming conventions were considered. In deciding between them, there were a number of considerations.

* Snake case has faster reading sped (i.e. easier).
* Snake case is awkward to type.
* All caps means shouting in common usage. It should be reserved for dangerous or rare things rather than used for common constants.
* It still makes sense to use a wider variety of casing conventions, but single word names mean that initial case must distinguish things that are truly important to distinguish.
* Acronyms have always been an issue in C# style naming conventions
* Namespaces only rarely occur inside code so it is less of a concern if they conflict with variables. Having them be distinct from types and functions in using statements is more valuable.
