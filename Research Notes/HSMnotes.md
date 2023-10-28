## Quick finite state machine review:
Processor does the following: fetch, decode, execute
* Fetch: read an instruction from memory, load into an instruction register
* Decode: figure out what instruction you read in
* Execute: do the instruction

*Note:* a traditional finite SMs doesn’t always have an instruction memory because they don’t usually have memory. The only bit of information that it’s allowed to know is what state is in

State machines help us model how a process goes from state to state when an event occurs. Each state can have associate actions, transitinos, and sub states. 

# HSMs
General idea: HSMs are like simple state machines, except they also have super states and can remember history. Superstates are composite states that encapsulate the behavior of a system. HSMs allow for the ability to implement multiple states in parallel with different regions running concurrently with one another. This allows for more complex applications and embedded systems. These are used in game dev, robotics, spacecraft, and any system that is complex where the managing of the states is crucial. HSMs have the capacity to remember history, where the machine 'remembers' the previous state of a substate or a region, enabling the system to return to the last active state if needed. They provide a clear and organized way to represent the behavior of a system, making it easier to understand, modify, and maintain software. 

## HSM Terms

**HSMs** - states can hold state machines. The states in a state machines can also hold them, these can be nested like crazy.
- In computation, HSMs are equivalent to FSMs
- Faulted event – forces the program to transition back to a previous state

Take an FSM that reads user input and also has a "bad" state. User inputs a, ends up in the bad state, then inputs b to leave the bad state. You can infer from that structure that any user input that starts with ab will let you out of the bad state and never go back in. Pushdown automata are equivalent to context-free grammars

*Event-handler sub-routines* - designed to handle a group of sub-routines (events)
*State* - state of a system in an *equivalence class* of past histories of a system, equivalent in the sense that the future behaviors of the system given any of the past histories will be identical
- State is the minimum relevant information that holds aspects for future behavior

*State machine* - A set of all states plus the rules for changing from one state to another. Events trigger a state transition

*State diagrams* - Different type of UML with the name of the state on the top. State transitions are represented as arrows labeled with the triggering event. *Internal transitions* do not cause state change, but do execute actions in response to a given event (ex: triggering event/action). Every state machine diagram needs an arrow signifying the initial state. 

*Run-To-Completion (RTC) event processing* - A state machine can only run one event at a time

*Guard conditions* - Represented with a diamond - A way to make state machines more flexible, expressed as booleans and evaluated at runtime. Traditionally, the structure of states and transitions is fixed and set at design time. What if the behavior is based on user input? -> *choice pseudostates and guard conditions*. 

*Nested States* - Made up of sub-states and superstates. If a substate handles a given event, it sill not be propogated back up to the superstate. This is a case where the substate overrides the behavior from the superstates. If the transition form the superstate is the one you want, then you can delete the transition from the overriding substate and rely on the main one. This is how state hierarchy allows you to get rid of repititous states. 

*Inheritance in HSMs (AKA Behavioral Inheritance)* - A mechanism for capturing commonalities in a higher-level superclass in order to reuse them in lower-level subclasses. Essentially substates inherit the behavior from their superstates. 

*Software Tracing* - the output from HSMs allows you to trace the code execution, which is helpful for testing debugging.

*leaf state* is the end of the substate train, meaning it has no further substates or nested intial states

Some quick notes:
- *Initial transitions* - represented as a solid circle - are able to cut through more than one level of state nesting
- Every state crossed by any transition must be properly entered. The explicit target of the transition is not the end of the trace.
- Any transition, including initial, needs to drill into the sub-states as long as there are initial transitions nested directly in the target state.

 ## Semantics
 - Top-most initial transition is attached to the transition itself. This transition can cut through nested states and reach the intended sub-state. Any state it cuts through must still be properly entered to get to the target state
    - Top-down entry action example where s2 is the target and s211 is the leaf state: top-INIT; s-ENTRY; s2-ENTRY; 2-INIT; s21-ENTRY; s211-ENTRY; where s21 and s211 are nested inside s2
 - The last entered state becomes the current state. This is when you can start dispatching events to your state machine
 - *Target State Configurationg example*: 
    - You type command "G" to dispatch event G into the state machine. The current state s211 (leaf state) doesn't have a transition labeled G, so it's passed to the next state up, s21. Since s21 has a transition labeled G, it executes the action associated with the transition. 
    - Next, the state machine executes the transition chain that *exits* the source state configuration and *enters* the target state config. 
    - The transition chain starts with exit actions from all states, traveling up the state heirarchy to the so-called *Least Common Ancestor (LCA)* but does not exit the LCA itself. All nested states within the superstate, but not the superstate itself, are exited
    - Next, the *target state config* is entered in the opposite order, starting from the highest level of hierarchy down to the lowest
- *Internal transitions vs Self transitions*
    - Self transitions in classic FSMs (where entry/exit actions don't exitst): a self-loop on a state is used to cause a reaction in that given state. 
    - Self transition- represented as an arrow leaving a state and circling back to the state - in HSMs is a term that refers to how a state is reset by exiting and re-entering the state
        - Ex: the 'cancel' button on a calculator
    - Internal transition - represented as a line ending at a square - don't have a change of state, doesn't execute exit or entry actions, it only specifies an action that needs to be taken when a certain event occurs

**Implementation Strategies**
- efficiency in time (CPU cycles)
- efficiency in data space (RAM footprint)
- efficiency in code space (ROM footprint)
- monolithic vs. partitioned with various levels of granularity
- maintainability (with manual coding)
- maintainability (via automatic code generation)
- traceability from design (e.g., state diagram) to code
- traceability from code back to design
- other, quality attributes (non-functional requirements)

**Active Objects**



    

