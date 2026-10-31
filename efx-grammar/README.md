# The `efx-grammar` folder

This folder contains the grammar of the eForms Expression Language (EFX).

EFX is a domain specific language (DSL) designed to be used for formally encoding validation rules, as well as visualisation templates for eForms notices. The grammar is designed to be used with the [ANTLR4](https://www.antlr.org/) parser generator.

Documentation of the eForms Expression Language can be found at <https://docs.ted.europa.eu/eforms/latest/efx>.

## How expressions are parsed

The grammar does not type expressions. One `expression` rule carries every operator, and the EFX translator infers the type of each part of an expression from its literals, from the field metadata of the SDK and from the declarations in scope, and rejects an expression whose types do not fit. Declarations keep their types, as in `text:$name = ...` or `number*:$values = ...`.

Operators bind in this order, tightest first:

1. Parentheses; the bracket after an expression, as in `BT-00-Text[...]` or `$list[1]`; and the steps after a reference: `/@attribute`, `::` (a field or node read from another context), `:rawValue`, `:preferredLanguage` and `:preferredLanguageText`.
2. `*`, `/` and `%`.
3. `+` and `-`.
4. The comparisons and conditions, each binding tighter than the next: `==`, `!=`, `<`, `<=`, `>`, `>=`, then `in`, `is unique in`, `is empty`, `has duplicates`, `like` and `is present`.
5. `and`.
6. `or`.
7. `if ... then ... else`, `every ... satisfies`, `some ... satisfies` and `for ... return`.

Two consequences for authors:

- The comparisons and conditions do not share a single level. `a == b in c` is read as `(a == b) in c`, so write parentheses when combining them.
- The expression after `else`, `satisfies` or `return` extends as far to the right as it can. `if c then 1 else 2 == 3` is read as `if c then 1 else (2 == 3)`; to compare the result of the conditional, write `(if c then 1 else 2) == 3`.
