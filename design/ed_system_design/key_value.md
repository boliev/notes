# Key-value Store

## Requirements
Let’s list the requirements of designing a key-value store to overcome the problems of traditional databases.

### Functional requirements
The functional requirements are as follows:
- Configurable service: Some applications might have a tendency to trade strong consistency for higher availability. We need to provide a configurable service so that different applications could use a range of consistency models. We need tight control over the trade-offs between availability, consistency, cost-effectiveness, and performance.
- Ability to always write: The applications should always have the ability to write into the key-value storage. If the user wants strong consistency, this requirement might not always be fulfilled due to the implications of the CAP theorem.
- Hardware heterogeneity: The system shouldn’t have distinguished nodes. Each node should be functionally able to do any task. Though servers can be heterogeneous, newer hardware might be more capable than older ones.

### Non-functional requirements
The non-functional requirements are as follows:
- Scalable: Key-value stores should run on tens of thousands of servers distributed across the globe. Incremental scalability is highly desirable. We should add or remove the servers as needed with minimal to no disruption to the service availability. Moreover, our system should be able to handle an enormous number of users of the key-value store.
- Available: We need to provide continuous service, so availability is very important. This property is configurable. So, if the user wants strong consistency, we’ll have less availability and vice versa.
- Fault tolerance: The key-value store should operate uninterrupted despite failures in servers or their components.