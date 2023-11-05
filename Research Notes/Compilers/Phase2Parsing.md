# Phase 2: Parsing

The Parser takes tokens and produces an Abstract Syntax Tree (AST)
- If you had a `vardec` node, it would have a child node with a type (ex: `int`), another for the `variable` (variable has it's own node with the name (ex: `"x"`)), and another for `number` (which holds `7`)