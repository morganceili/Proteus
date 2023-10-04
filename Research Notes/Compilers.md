## Compilers

Programming languages generally run either through an interpreter or a compiler
    *Interpreted Style*
    - Interpreter takes the 'input program' (e.g. Python), as well as 'program input' (e.g. numbers for a caculation)
    - The interpreter essentially is a program that looks at the Python code and does what it says to do.
    - Interpreter then gives you back the program output

    *Compiled Style*
    - Compiler 'input program' (e.g. C) goes into the compiler, and the compiler *translates* it to an intermediate language (like machine code), where it then goes into an interpreter to give the program output
    - A processor (which reads machine code) can be seen as an interpreter, it's just an interpreter that was built off of circuits instead of code

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

**stopped at 24:48** 

    
