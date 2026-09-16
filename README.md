# strutil

String helpers for candela programs.

Use it when a program quotes a value or an identifier for another language,
checks that a string is a number or an identifier, splits text into words,
strips a prefix or suffix, changes case, or trims, indents, and truncates
text for display. It has no dependencies and works the same everywhere.

## Quick start

```sh
candela add strutil
```

```rust
import "strutil" as strutil;

fn main() {
    print("user name".quote_ident());          // "user name"
    print("it's".quote_literal());             // 'it''s'
    print(strutil::placeholders(3));           // ?, ?, ?
    print("camelCaseName".to_snake());         // camel_case_name
}
```

The methods live on `string`, so a bare `import "strutil";` brings them in
with no prefix. The free functions are reached through the alias.

## What it provides

Methods on `string`:

- `quote_ident()`, `quote_literal()`: SQL quoting with the quote doubled.
- `strip_prefix(p)`, `strip_suffix(s)`: remove a prefix or suffix when present.
- `is_digits()`, `is_identifier()`: shape checks for parsing input.
- `truncate(width, ellipsis)`: cut to a width, ending in the ellipsis.
- `words()`: whitespace-separated words, no empties.
- `indent(prefix)`: prefix every line.
- `to_snake()`: camelCase or PascalCase to snake_case.

Free functions:

- `placeholders(n)`: `?, ?, ?` for a values list.
- `join_idents(names)`: quoted identifiers joined with commas.

## Limitations

Indices count bytes, as candela strings do, so `truncate` cuts a multi-byte
character in half when the width lands inside one.

## Tests

```sh
candela run tests/test_strutil.cdl
```
