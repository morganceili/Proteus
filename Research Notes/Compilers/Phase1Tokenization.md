# Phase 1: Tokenizing

**Language Design** (tokens are defined shortly after the grammer is defined)
- var is a Variable
- num is a Number
- type ::= `int` | `bool`
- vardec ::= (`vardec` type var -expression )
- expression ::= num | `true` | -`false`| (`operator expression expression`)`
- loop ::= (`while` expression -statement)
- assign ::= (`=` var expression )
- statement ::= vardec | loop | assign
- op ::= `+` | `-` | `&&` | `||`
- program ::= statement*

(vardec int x 7)                //int x = 7
(vardec bool y true)            //boolean y = true
(vardec int a(+12))             //int a = 1 + 2
(vardec bool b(&& false true))  //boolean b = false&&true

- Types are either ints or bools
- Declare and initizliae variables
- Perform typical arithmetic and logical operations

**Possible Tokens** for the above language design
- IdentifierToken (String)
- NumberToken (int)
- IntToken
- BoolToken
- LeftParenToken, RightParenToken
- VardecToken
- TrueToken, FalseToken
- WhileToken
- SingleEqualsToken
- PlusToken, MinusToken
- LogicalAndToken, LogicalOrToken, LessThanToken

*Ex*: (vardec int x 7) 
    - LeftParenToken
    - VardecToken
    - IntToken
    - IdentifierToken("x")
    - NumberToken(7)
    - RightParenToken

- *Tokens and Idendifier tokens*
    - Tokens: ActorToken, StateToken, NumberToken 
        - `2 + 3 <-- NumberToken(2), PlusToken, NumberToken(3)`
    - Identifier Tokens are another kind of token that usually contain a name 
        - `int x = 2 + 3 <-- IntToken, IdentifierToken("x"), EqualsToken, NumberToken(2), etc.`

**Important Note: Pokemon Yellow is Turing Complete** 