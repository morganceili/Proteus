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