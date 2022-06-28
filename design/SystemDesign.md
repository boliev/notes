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

Causal consistency works by categorizing operations into dependent and independent operations. Dependent operations are also called causally-related operations. Causal consistency preserves the order of the causally-related operations.
Causal consistency is weaker overall, but stronger than the eventual consistency model. It’s used to prevent non-intuitive behaviors.

#### Example

The causal consistency model is used in a commenting system. For example, for the replies to a comment on a Facebook post, we want to display comments after the comment it replies to. This is because there is a cause-and-effect relationship between a comment and its replies.

### Sequential consistency

Sequential consistency is stronger than the causal consistency model. It preserves the ordering specified by each client’s program. However, sequential consistency doesn’t ensure that the writes are visible instantaneously or in the same order as they occurred according to some global clock.

#### Example

In social networking applications, we usually don’t care about the order in which some of our friends’ posts appear. However, we still anticipate a single friend’s posts to appear in the correct order in which they were created).

### Strict consistency aka Linearizability

A strict consistency or linearizability is the strongest consistency model. This model ensures that a read request from any replicas will get the latest write value. Once the client receives the acknowledgment that the write operation has been performed, other clients can read that value.
Linearizability affects the system’s availability, which is why it’s not always used

#### Example

Updating an account’s password requires strict consistency. For example, if we suspect suspicious activity on our bank account, we immediately change our password so that no unauthorized users can access our account. If it were possible to access our account using an old password due to a lack of strict consistency, then changing passwords would be a useless security strategy.
Amazon Aurora provides strong consistency.

## Reliability and availability

### Availability

Availability is the percentage of time that some service or infrastructure is accessible to clients and is operated upon under normal conditions. For example, if a service has 100% availability, it means that the said service functions and responds as intended (operates normally) all the time.

### Reliability

Reliability, `R`, is the probability that the service will perform its functions for a specified time. `R` measures how the service performs under varying operating conditions.
We often use mean time between failures (MTBF) and mean time to repair (MTTR) as metrics to measure `R`.

Reliability (`R`) and availability (`A`) are two distinct concepts, but they are related. Mathematically, `A` is a function of `R`. This means that the value of `R` can change independently, and the value of `A` depends on `R`. Therefore, it’s possible to have situations where we have:

- low `A`, low `R`
- low `A`, high `R`
- high `A`, low `R`
- high `A`, high `R` (desirable)

## Scalability

Scalability is the ability of a system to handle an increasing amount of workload without compromising performance. A search engine, for example, must accommodate increasing numbers of users, as well as the amount of data it indexes.

The workload can be of different types, including the following:

- Request workload: This is the number of requests served by the system.
- Data/storage workload: This is the amount of data stored by the system.

### Dimensions

- *Size scalability*: A system is scalable in size if we can simply add additional users and resources to it.
- *Administrative scalability*: This is the capacity for a growing number of organizations or users to share a single distributed system with ease.
- *Geographical scalability*: This relates to how easily the program can cater to other regions while maintaining acceptable performance constraints. In other words, the system can readily service a broad geographical region, as well as a smaller one.

### Approaches of scalability

- Vertical scaling, also known as “scaling up,” refers to scaling by providing additional capabilities (for example, additional CPUs or RAM) to an existing device. Vertical scaling allows us to expand our present hardware or software capacity, but we can only grow it to the limitations of our server. The dollar cost of vertical scaling is usually high because we might need exotic components to scale up.
- Horizontal scaling, also known as “scaling out,” refers to increasing the number of machines in the network. We use commodity nodes for this purpose because of their attractive dollar-cost benefits. The catch here is that we need to build a system such that many nodes could collectively work as if we had a single, huge server.

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