# System design

https://www.educative.io/courses/grokking-modern-system-design-software-engineers-managers

System design aims to build systems that are reliable, effective, and maintainable, among other characteristics.
- Reliable systems handle faults, failures, and errors.
- Effective systems meet all user needs and business requirements.
- Maintainable systems are flexible and easy to scale up or down. The ability to add new features also comes under the umbrella of maintainability.

## Consistency

### What is consistency?

#### In ACID

If a schema specifies that a value must be unique, a consistent system will ensure that the value is unique throughout all actions. If a foreign key indicates that deleting one row will also delete associated rows, a consistent system ensures that the state can’t contain related rows once the base row has been destroyed.

#### In CAP

Each replica node has the same view of data at a given point in time, each read request gets the value of the recent write.

### Eventual consistency

the weakest consistency model. The applications that don’t have strict ordering requirements and don’t require reads to return the latest write choose this model. Eventual consistency ensures that all the replicas will eventually return the same value to the read request, but the returned value isn’t meant to be the latest value. However, the value will finally reach its latest state.
The *domain name system* is a highly available system that enables name lookups to a hundred million devices across the Internet. It uses an eventual consistency model and doesn’t necessarily reflect the latest values.
*Cassandra* is a highly available NoSQL database that provides eventual consistency.

### Causal consistency

## ACID

Atomicity, Consistency, Isolation, and Durability

## What is the CAP theorem?

https://www.educative.io/answers/what-is-the-cap-theorem
The CAP theorem (also called Brewer’s theorem) states that a distributed database system can only guarantee two out of these three characteristics: Consistency, Availability, and Partition Tolerance.
*Consistency* - A system is said to be consistent if all nodes see the same data at the same time.
*Availability* - in a distributed system ensures that the system remains operational 100% of the time. Every request gets a (non-error) response regardless of the individual state of a node.
*Partition Tolerance* - This condition states that the system does not fail, regardless of if messages are dropped or delayed between nodes in a system. Partition tolerance has become more of a necessity than an option in distributed systems. It is made possible by sufficiently replicating records across combinations of nodes and networks.

## Other

 principal engineers or solution architects

 https://www.educative.io/courses/distributed-systems-practitioners
 https://www.educative.io/courses/grokking-computer-networking
 https://www.educative.io/courses/operating-systems-virtualization-concurrency-persistence