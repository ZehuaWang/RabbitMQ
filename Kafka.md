# Apache Kafka

A high-throughput distributed messaging system.

A tyipical enterprise 

![image](https://user-images.githubusercontent.com/40006814/160299160-10b27b75-9337-4cd5-a9ef-4955d1147d2b.png)

To move data around:

Cleanly, Reliably, Quickly Autonomously

Next-generation Messaging Goals

High Throughput

Horizontally scalable

Reliable and durable

Loosely coupled Producers and Consumers

![image](https://user-images.githubusercontent.com/40006814/160299890-9620615c-e961-4977-a88c-83b1ffb1300a.png)

Kafka is a distributed messaging system

Designed to move data at high volumes

Addresses shortcomings of traditional data movement tools and approaches

Invented by LinkedIn to address data growth issues common to many enterprises

Open-sourced under Apache Foundation

## Getting to know Apache Kafka Architecture

![image](https://user-images.githubusercontent.com/40006814/160306159-6b6da249-35ff-4b66-b61a-0407db4be159.png)

![image](https://user-images.githubusercontent.com/40006814/160306211-d7be2c9e-b184-4bd3-bdbd-d1098cb90904.png)

![image](https://user-images.githubusercontent.com/40006814/160306345-b52434b5-c50c-40df-acd7-b598fbe127f3.png)

![image](https://user-images.githubusercontent.com/40006814/160306211-d7be2c9e-b184-4bd3-bdbd-d1098cb90904.png)

![image](https://user-images.githubusercontent.com/40006814/160306743-88bbb318-9013-4dc9-b701-696ad1c41928.png)


![image](https://user-images.githubusercontent.com/40006814/160306708-f9b90fd4-6e03-4178-b116-a844f3500670.png)

Distributed Systems: Communication and Consensus

1. Worker node membership and naming
2. Configuration management
3. Leader election
4. Health status

Apache Zookeeper

Centralized service for maintaning metadata about a cluster of distributed nodes

- Configuration information
- Health status
- Group membership

Hadoop, HBase, Solr, Redis and Neo4j

Distributed system consisting of multiple nodes in an "ensemble"

![image](https://user-images.githubusercontent.com/40006814/160307044-386eb2ec-45fc-43dc-ab6c-42a2429cbca3.png)

Summary:

Apache Kafka is a Pub-Sub messaging system, consisting of:
- Producers and Consumers
- Brokers within a Cluster

Characteristics of distributed systems:
- Worker node roles: Controllers, Leaders, and Followers
- Reliability through replication
- Consensus-based communication

Role of Apache Zookeeper

## Getting Started with Apache Kafka

Apache Kafka Topics

Central Kafka abstraction

Named feed or category of messages

- Producers produce to a topic
- Consumers consume from a topic

Logical entity

Physically reprensented as a log

![image](https://user-images.githubusercontent.com/40006814/160473714-aefe524c-8719-4321-b373-a4ff84eadc3d.png)

![image](https://user-images.githubusercontent.com/40006814/160473840-f94b2e72-5bcb-4edb-b816-6c3c61e80e64.png)

Event Sourcing

An architectural style or approach to maintaining an application's state by capturing all changes as a sequence of time-ordered, immutable events.

Each message has a:

- Timestamp
- Referenceable identifier
- Payload (binary)

The Offset

A placeholder:
- Last read message position
- Maintained by the Kafka Consumer
- Corresponds to the messaging identifier

Message Retention Policy

Apache Kafka retains all published messages regardless of consumption

Retention period is configurable
  - Default is 168 hours or serven days

Retention period is defined on a per-topic basis

Physical storage resources can constrain message retention

Kafka Partitions:

![image](https://user-images.githubusercontent.com/40006814/160911730-4b112ed6-bb24-4aea-9015-936bdc964467.png)

![image](https://user-images.githubusercontent.com/40006814/160912138-2d510b47-bb8d-4486-9e29-649861724f56.png)

In general, the scalability of Apache Kafka is determined by the number of partitions being managed by multiple broker nodes.

![image](https://user-images.githubusercontent.com/40006814/160912617-c1512ce0-85e2-444e-b8ca-0b88c43741a2.png)

With 3 partitions, we are causing a single topic to be split across three different log fiels. Ideally managed by three different broker nodes. Each partition is mutually exclusive from one another in that they receive unique messages from a Kafka producer producing on the same topic. This enables each partition to share the burden of the message load across multiple broker nodes and increase the parallelism of certain operations like message consumption. 

![image](https://user-images.githubusercontent.com/40006814/160913278-6bb919e0-830b-4e78-9bb1-8c9ce32c5427.png)

With 3 partitions, we are causing a single topic to be split across three different log fiels. Ideally managed by three different broker nodes. Each partition is mutually exclusive from one another in that they receive unique messages from a Kafka producer producing on the same topic. This enables each partition to share the burden of the message load across multiple broker nodes and increase the parallelism of certain operations like message consumption. 


![image](https://user-images.githubusercontent.com/40006814/160926843-180b6f16-a280-420a-99f7-9eee37b211d5.png)

Partition Trade-offs

The more partitions the greater the Zookeeper overhead

- With large partition numbers ensure proper ZK capacity

Message ordering can become complex

- Single partition for global ordering
- Consumer-handling for ordering

The more partitions the longer the leader fail-over time
