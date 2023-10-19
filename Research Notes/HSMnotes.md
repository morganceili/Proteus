### Quick finite state machine review:
Processor does the following: fetch, decode, execute
* Fetch: read an instruction from memory, load into an instruction register
* Decode: figure out what instruction you read in
* Execute: do the instruction

*Note:* a traditional finite SMs doesn’t always have an instruction memory because they don’t usually have memory. The only bit of information that it’s allowed to know is what state is in

## HSMs
**HSMs** - states can hold state machines. The states in a state machines can also hold them, these can be nested like crazy.
- In computation, HSMs are equivalent to FSMs
- Faulted event – forces the program to transition back to a previous state

Take an FSM that reads user input and also has a "bad" state. User inputs a, ends up in the bad state, then inputs b to leave the bad state. You can infer from that structure that any user input that starts with ab will let you out of the bad state and never go back in. Pushdown automata are equivalent to context-free grammars

*Event-handler sub-routines* - designed to handle a group of sub-routines (events)
*State* - state of a system in an *equivalence class* of past histories of a system, equivalent in the sense that the future behaviors of the system given any of the past histories will be identical
- State is the minimum relevant informatin that holds aspects for future behavior

*State machine* - A set of all states plus the rules for changing from one state to another. Events trigger a state transition

*State diagrams* - Different type of UML with the name of the state on the top. State transitions are represented as arrows labeled with the triggering event. *Internal transitions* do not cause state change, but do execute actions in response to a given event (ex: triggering event/action). Every state machine diagram needs an arrow signifying the initial state. 

*Run-To-Completion (RTC) event processing* - A state machine can only run one event at a time

*Guard conditions* - A way to make state machines more flexible, expressed as booleans and evaluated at runtime. Traditionally, the structure of states and transitions is fixed and set at design time. What if the behavior is based on user input? -> *choice pseudostates and guard conditions*. 

*Nested States* - Made up of sub-states and superstates. If a substate handles a given event, it sill not be propogated back up to the superstate. This is a case where the substate overrides the behavior from the superstates. If the transition form the superstate is the one you want, then you can delete the transition from the overriding substate and rely on the main one. This is how state hierarchy allows you to get rid of repititous states. 

*Inheritance in HSMs (AKA Behavioral Inheritance)* - A mechanism for capturing commonalities in a higher-level superclass in order to reuse them in lower-level subclasses. Essentially substates inherit the behavior from their superstates. 
