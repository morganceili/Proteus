## Compilers

Programming languages generally run either through an interpreter or a compiler

 *Interpreted Style*
- Interpreter takes the 'input program' (e.g. Python), as well as 'program input' (e.g. numbers for a caculation)
- The interpreter essentially is a program that looks at the Python code and does what it says to do.
- Interpreter then gives you back the program output

*Compiled Style*
- Compiler 'input program' (e.g. C) goes into the compiler, and the compiler *translates* it to an intermediate language (like machine code), where it then goes into an interpreter to give the program output
- A processor (which reads machine code) can be seen as an interpreter, it's just an interpreter that was built off of circuits instead of code

- *Reserved Word* - a word that always has a certain meaning regardless of context. For example in Java, "while" cannot be delcared as a variable because it's reserved for loops
- *Keyword* - weaker, they are context-sensitive. 

------------------------------------------------------------------

A compiler is usually structured with multiple phases:
- **Phase 1 - Tokenizer/Lexer** takes an input program and breaks it into tokens
    - *Token*:  individual tokens are like individual words in a sentence (possible tokens include 'if', 'while', 'for', etc.)
- **Phase 2 - Parser** takes tokens and groups them together and represents them as a tree-like data structure
   - Output: Abstract Syntax Tree (AST) - a representation of the original program as a tree
    ```
    if (1<2){
        return 7;    
    } else{              
        return 3;
    }
    ```
     >this if/else can be represented as a tree where each node is a decision/path the program can take
- **Phase 3 - Typechecker** looks at all the types involved and checks that they are well-typed. If yes, it will add type annotations (Annotated AST), and pass it to the code generator
- **Phase 4 - Code Generator** is the thing that actually does the translation. For mainstream languages, this is the most complicated part, it can make or break how good the compiler is. 

------------------------------------------------------------------

**Grammar / Backus-Naur Form / Context-Free Grammar** (usually done before the tokens are defined)
- digit ::= `0` | `1`
- number ::= digit | digit number (translates to digit OR digit AND number)
- number ::= digit* (EBF form - * means 0 or more of the thing tha precedes it)
- expression ::= number | expression `+` expression
- example numbers: 0, 1, 01, 101
- example expressions: 1101, 101 + 110, (1 + 111) + (01 + 10)

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

-------------------------------------------------------------------

## Proteus Grammar Notes
List of production rules
`Production Rule Name: Production1 | Production2 | ... | ProductionN`
- `ActorItem: DefHSM | DefActorOn` <-- Actor Item can be one of these two things
- `Program: DefEvent* DefActor+` <-- Zero or more DefEvents, one or more DefActors
- ActorName: NAME <-- Aything in caps is a token. There is a "name" token provided by the tokenizer
- `DefActor: 'actor' ActorName '{' ActorItem* '}'` <-- Anything within single quotes is something written directly into the grammar
	- *Ex* `actor Foo { ... }` where the ActorItem in between braces can be any of the things listed for the ActorItem production rule



    
