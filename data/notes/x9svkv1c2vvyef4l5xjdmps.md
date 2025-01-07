
## Command and Query Responsibility Segregation

CQRS means to segrate the responsibility between commands (write requests) and queries (read requests).

Commands and queries don't need to be run on separate databases, only the responsibility and behaviours should be separate within the code. Different databases can be used to optimize reads or writes according to needs.

Commands are events that took place in the domain. They are usually named with past-participle verbs e.g. OrderConfirmed

Commands are requests for changes to the domain. They are usually named with a verb e.g. ConfirmOrder

Commands and events are just data structures with no behaviour. They are called "Data Transfer Objects" (DTOs).

Aggregates are a larger unit of encapsulation that handles commands, applies events and have a state model encapsulated within that allows it to implement the required command validation.

A command handler receives a command and brokers a result from the appropriate aggregate.

#### Event sourcing

Storing all the changes (events) to the system rather than just its current state.

Event sourcing is not a requirement to do CQRS but it works well with it.
