## Proteus
Language developed in collaboration with JPL. Similar to C, intended for aerospace 
o	Constraints are very critical – must be able to work since we can’t access things once they’re in space
-	Built-support for actors, HSMs, and runtime monitors (used for runtime verification)
-	It has variables and functions, but also monitors, exclamation points, actors, states, weird things

*Actors:* a model used in parallel programming – meaning it’s used for multiple computers, multiple processors, multiple cores. This means the programs have to be written to be able to utilize multiple cores (machine-to-machine comms)
- each actor has some state, and that state is internal (only that actor can change the state)
- Independent units that can execute in parallel
- actors communicate by passing messages/sending events to each other
- characterized by “get some event, process that event, and do that forever”. These messages are processed one at a time

*Events:* beginning of the code needs to list all of the types of events that are possible, or messages that are possible
- Events can hold data (ints, strings, etc.)
- ! is used to send an event 
•	**System ! READY{};** sends “ready” event to “system”
•	Semantically, each actor acts independently from other actors. This means each core could be utilized for a single actor (gives you total utilization of the hardware)

### 9/29

Actors support “runtime monitors” where it watches the execution of a state machine and does something in response to what another state machine does

	monitor Property1 {
		state machine {
			code
		}
    }

**on _ENTRY{a,s}** – a is actor, s is state, ‘do this thing upon entry’

*Object Language:* refers to the input language of a compiler
    - Ex: Java is the object language of javaC 

*Metalanguage:* the language the compiler is implemented in (the lang used in the translator/compiler)
	- Ex: Java is the metalanguage for javac
	- Ex: cpython is written in C, C is the metalanguage of python 

*Target language:* output language of a compiler
-	Ex: Java bytecode is the target language for javac
-   Ex: Java bytecode is the target language for scalac
-   Java bytecode doesn’t have anything specific saying it has to be Java

Usually, translators have to know both languages (think Japanese to English). In our case, the compiler is the translator 

You can have both language versions and compiler versions. This separates the behavior of the language from the implementation of the language itself


## Proteus compiler V1:
-	Input program (proteus language), output is C++
-	Object language: Proteus
-   Metalanguage: C++ 
-   Target Language: C++ 

Input program -> tokenizer (moves tokens to parser) -> 
Parser -> abstract syntax tree (AST – used to understand sentences) -> typechecker 
	- Parser -> code generator (takes AST input and generates the C++ output code)

## Proteus compiler V2:
-   Object language: Proteus
-   Metalanguage: Swift (because C++ is not a good lang to build compilers in)
-   Target language: C/C++

## Proteus Grammar Notes
*Grammar / Backus-Naur Form / Context-Free Grammar* (usually done before the tokens are defined)
- digit ::= `0` | `1`
- number ::= digit | digit number (translates to digit OR digit AND number)
- number ::= digit* (EBF form - * means 0 or more of the thing tha precedes it)
- expression ::= number | expression `+` expression
- example numbers: 0, 1, 01, 101
- example expressions: 1101, 101 + 110, (1 + 111) + (01 + 10)
*Proteus:*
List of production rules
`Production Rule Name: Production1 | Production2 | ... | ProductionN`
- `ActorItem: DefHSM | DefActorOn` <-- Actor Item can be one of these two things
- `Program: DefEvent* DefActor+` <-- Zero or more DefEvents, one or more DefActors
- ActorName: NAME <-- Aything in caps is a token. There is a "name" token provided by the tokenizer
- `DefActor: 'actor' ActorName '{' ActorItem* '}'` <-- Anything within single quotes is something written directly into the grammar
	- *Ex* `actor Foo { ... }` where the ActorItem in between braces can be any of the things listed for the ActorItem production rule
