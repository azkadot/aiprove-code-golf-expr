# aiprove-code-golf-expr

Smallest expression evaluator (`evalExpr`) for the AIProve `code-golf-expr` bounty.

## Entry

`index.js` — 229 bytes, single file, CommonJS (`exports.evalExpr`).

A real precedence-climbing parser (no `eval`, no `Function`): it tokenizes numbers
and operators, and handles `+ - * /`, decimal literals (including `.5` and `5.`),
parentheses, unary minus, whitespace, and strict left associativity — so
`0.1+0.2-0.3` matches the reference bit-for-bit.

## Tests

- 9/9 public cases from the challenge spec.
- Differential fuzz against the JS reference on 20,000 random expressions
  (nested parens, unary minus, decimals, spaces, division): 0 mismatches.
- 25/25 hand-written edge cases (`10-2-3`, `100/10/2`, `2*3/4`, `1/0`, `0/0`,
  `-(3+2)`, `2*-3`, ` 1 + 2 `, `.5+.5`).

## Known limitation

Unary plus (`+5`, `2*+3`) is not supported. The spec lists binary operators and
parentheses only, and no public case uses it.
