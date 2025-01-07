
Topics that don't necessarily fit into just FE or BE e.g. repo management, CI/CD, devops.

## Types of Architectures

### Monolithic Architecture

A single server application
responsible for all the features of the system e.g. a hotel application could have a single application taking care of payments, bookings, campaign offers and so on. This is a common way for applications to start out and even continue if they are simple or non-complex.

### Microservices Architecture

Splitting out responsibility into multiple application servers e.g. one for payments, one for streaming, one for recommendations.

This allows us to scale individual services and prevent code from becoming too complex by making use of single responsibility principles and loose coupling.

Microservices architecture is more complex to set up and manage and is therefore more useful for larger projects.

## Patterns and Design Principles

### Command Query Responsibility Segregation (CQRS)

A pattern that separates the responsibility of reading (querying) data and modifying (commanding) the data. On the command side, CQRS emphasizes the use of commands to perform action that modify application state. The traditional alternative to CQRS is CRUD (create, read, update delete) where the same services are responsible for the handling of all operations.

On the query side, CQRS emphasizes the use of queries to retrieve data from the system. These are typically handled by query handlers within the system.

The main advantage of separating command and query is giving developers the ability to optimize each side independently. Read can be optimized with strategies such as caching or specialized data stores. CQRS is useful in complex domains or applications where read and write have different scalability and performance requests. Considering it adds complexity would mean that it's not suitable for all requirements and trade-offs should be taken into account.

[[Read more|architecture.CQRS]]

### ACID & CAP Theorem

ACID (Atomic, Consistency, Isolation, Durability) and CAP (Consistency, Availability, Partition Tolerance) are concepts in distributed systems that are used to explain the trade offs between consistency and availability.

According to the CAP theorem, any distributed system can only guarantee two of three properties at a time. You can't guarantee all three properties at once:

<img src="https://miro.medium.com/v2/resize:fit:1400/format:webp/1*Br1FrvKnK3hU6Xl_LbDkwg.png">

ACID is a set of properties of database transactions intended to guarantee validity even in the event of errors, power failures, etc.
