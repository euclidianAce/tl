
This is a constructive approach to define a `comptime` construct for the teal language

# Expressions
## Primitives/Literals
 - Literals are trivially compile time known, this includes:
    - numbers
    - booleans
    - strings

Binary operations between comptime known expressions are comptime themselves
 - concatenation
 - arithmetic operations
 - logic operations

A toplevel `...` by definition can not be comptime

# Simple Statements

- A statement is comptime iff all contained expressions are comptime
- global declarations can never be comptime
- local declarations are comptime iff every variable is annotated as `<comptime>`
- return statements are comptime if each expression returned is comptime

- type definitions are comptime

# Compound statements

A do-end block is comptime iff all of its statements are comptime

if statements are comptime iff
 - each statement in the initial block is comptime
 - if any elseifs are present: each statement in each elseif is comptime
 - if an else is present: each statement in the else block is comptime

numeric for loops are comptime iff
 - each expression defining the range is comptime
 - each statement in the body is comptime

generic for loops are comptime iff
 - the iterator is comptime
 - each statement in the body is comptime

while/repeat-until loops are comptime iff
 - the condition expression is comptime
 - each statement in the body is comptime

This lets us define function definitions as comptime iff
 - given that the arguments are comptime => each statement in the function definition is comptime
A comptime function definition is a comptime expression

Function calls of comptime functions with comptime arguments are comptime expressions
