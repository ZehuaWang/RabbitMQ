# Java Message Service

## What is Java message service
Enterprise messaging systems are used to send notification of
events and data between software applications.

There are two common programming models supported by the JMS API: publish-and-subscribe and point-to-point. Each model provides benefits and either or both may be implemented by JMS providers.

Pros: asynchronous messaging system and no need for tightly coupled.

## Understand the messaging Paradigm

Enterprise messaging system allow two or more applications to exchange information in the form of messages. A message, in this case, is a self-contained package of business data and network routing headers. In enterprise messaging system, messages inform an application of some event or occurrence in another system.

Using Message-Oriented Middleware, message are transmitted from one application to another across a network. MOM products ensure that messages are properly distributed among applications. In addition, MOMs usually provide fault tolerance, load balancing, scalability, and transactional support for enterprise that need to reliability exchange large amount of messages.

In all modern enterprise messaging system, applications exchange messages through virtual channels called destinations. When a message is sent, it's addressed to a destination, not a specific application. Any application that subscribe or registers an interest in that destination may receive that message. In this way, the applications that receive messages and those that send messages are decoupled.

The Java Message Service (JMS) is a vendor-agnostic Java API that can be used with many different MOM vendors.

## Enterprise Messaging
A key concept of enterprise messaging is messages are delivered asynchronously from one system to others over a network.

To deliver a message asynchronously means the sender is
not required to wait for the message to be received or handled by the recipient; it is free to send the message and continue processing. Asynchronous messages are treated as autonomous units - each message is self-contained and carries all of the data and state needed by the business logic that processes it.

Message-Oriented-MiddleWare

![Message-Oriented-MiddleWare](https://user-images.githubusercontent.com/40006814/160046542-00fa71da-bdfc-4220-9258-da5679fbe680.png)

Messaging systems are composed of messaging clients and some kind of
MOM. The clients send messages to the MOM, which then distributes those messages to
other clients. The client is a business application or component that is using the messaging
API (in our case JMS).

### Centralized Architectures

Enterprise messaging system that use a centralized architecture rely on a message server. A message server, also called a message router or broker, is responsible for delivering message from one messaging client to other messaging clients. The message server decouples a sending client from other receiving clients. Clients only see the messaging server, not other clients, which allows clients to be added and removed without impacting the system as a whole.

Typically, a centralized architecture uses a hub-and-spoke topology.

![Centralized hub-and-spoke architecture](https://user-images.githubusercontent.com/40006814/160248774-9df41f59-ff7b-4e80-8357-08697a8bc747.png)

### Decentralized Architectures

All decentralized architectures currently use IP multicast at the network level. A messaging system based on multicasting has no centralized server. Some of the server functionality(persistence, transactions, security) is embedded as a local part of the client, while message routing is delegated to the network layer by using the IP multicast protocol. IP multicast allows applications to join one or more IP multicast groups; each group uses an IP network address that will redistributed any messages it receives to all members in its group. In this way, applications can send messages to an IP multicast address and expect the network layer to redistributed the messages appropriately. 

![Decentralized IP multicast architecture](https://user-images.githubusercontent.com/40006814/160249043-a1579b56-0a27-4fda-b7f8-72f1fa47c60c.png)

### Hybrid Architectures

A decentralized architecture usually implies that an IP multicast protocol is being used. A centralized architecture usually implies that the TCP/IP protocol is the basis for communication between the various components. A messaging vendor's architecture may also combine the two approaches. Clients may connect to a daemon process using TCP/IP, which in turn communicate with other daemon process using IP multicast groups.

In centralized architectures, the message server is a middleware server or cluster of servers. In decentralized architectures, the server refers to the local server-like facilities of the client.

### The Java Message Service (JMS)

The Java Message Service (JMS) is an API for enterprise messaging created by Sun Microsystems. JMS is not a messaging system itself; it is an abstraction of the interfaces and classes needed by messaging clients when communication with messaging systems. In the same way that JDBC abstract access to relational databases and JNDI abstract access to naming and directory services, JMS abstracts access to MOMs. Using JMS, a messaging application's messaging clients are portable across MOM products.

### JMS Messaging Models: Publish-and-Subscribe and Point-to-Point

JMS provides for two types of messaging models, publish-and-subscribe and point-to-point queueing. The JMS specification refers to these as messaging domains. 

In the simplest sense, publish-and-subscibe is intended for a one-to-many broadcast of messages, while point-to-point is intended for one-to-one delivery of messages.

![JMS messaging domains](https://user-images.githubusercontent.com/40006814/160250484-8c80ec4f-9b5a-40d9-9862-8f37a435fef3.png)

Messaging clients in JMS are called JMS clients, and the messaging system - the MOM - is called the JMS provider. A JMS application is a business system composed of many JMS clients and, generally, one JMS provider.

In addition, a JMS client that produces a message is called a producer, while a JMS client that receives a message is called a consumer. A JMS client can be both a producer and a consumer.

### Publish-and-subscribe

In pub/sub, one producer can send a message to many consumers through a virtual channel called a topic. Consumers, which receive messages, can choose to subscribe to a topic. Any messages addressed to a topic are delivered to all the topic's consumers. Every consumer receive a copy of each message. The pub/sub messaging model is by and large a push-based model, where messages are automatically broadcast to consumers without them having to request or poll the topic for new messages.

### Point-to-point

The point-to-point messaging model allos JMS clients to send and receive messages both synchronously and asynchronously via virtual channels known as queues. The p2p messaging model has traditionally been a pull or polling-based model, where messages are requested from the queue instead of being pushed to the client automatically. 

A given queue may have multiple receivers, but only one receiver may consume each message. The JMS specification does not dictate the rules for distributing messages among multiple receivers, although some JMS vendors have chosen to implement this as a load balancing capability. P2p also offers other features, such as a queue browser that allows a client to view the contents of a queue prior ro consuming its message - this browser concept is not available in the pub/sub model.

### Building Dynamic Systems with Messaging and JMS

In JMS, pub/sub topics and p2p queues are centrally administered and are referred to as JMS administered objects. The application does not need to know the network location of topics or queue to communicate with other applications; it just uses topic and queue objects as identifiers. Using topics and queues provides JMS applications with a certain level of location transparency and flexibility that makes it possible to add and remove participants in an enterprise system.

For example, a system administrator can dynamically add subscribers to specific topics on an as-needed basis. A common scenario might be if you discrover a need to add an auditrail mechanism for certian messages and not others. The figure shows you how to plug in a specialized auditing and logging JMS client whose only job is to track specific messages, just by subscribing to the topics you are interested in.

The ability to add and remove producers and consumers allows enterprise system to dynamically alter the routing and re-routing of messages in an already deployed environment.

![image](https://user-images.githubusercontent.com/40006814/160251679-322d8660-0728-4d6c-aff1-c4c50032428d.png)

### Enterprise Messaging

A fundamental concept of MOM is that communication between applications is intended to be asynchronous. Code that is written to connect the pieces together assumes there is a one-way message that requires no immediate response from another application. In other words, there is no blocking. Once a message is sent, the messaging client can move on to other tasks. It does not have to wait for a response. This is the major difference between RPC and asynchronous messaging, and is critical to understanding the advantages offered by MOM systems.

In an asynchronous messaging system, each subsystem (Accounts, Inventory) is decoupled from the other systems. They communicate through the messaging server, so that a failure in one does not impede the operation of others.

![image](https://user-images.githubusercontent.com/40006814/160251865-ce9b2d7e-e1d0-40b3-ab65-23fb01f61d16.png)

Partial failure in a networked system is a fact of life. One of the systems may have an unpredictable failure or need to be shut down at some time during its continuous operation. In recognition of this, JMS provides guaranteed delivery, which ensures that intended consumers will eventually receive a message even if partial failure occurs.

Guaranteed delivery uses a store-and-forward mechanism, which means that the underlying message server will write the incoming messages out to a presistent store if the intended consumers are not currently available. When the receiving applications become available at a later time, the sotre-and-forward mechanism will deliver all of the messages that the consumers missed while unavailable.

![image](https://user-images.githubusercontent.com/40006814/160252031-f72217ff-53bc-4fa2-96c4-c86f8cb48387.png)

To summarize, JMS is not just another event service. It was designed to cover a broad range of enterprise applications, including EAI, B2B, push models, etc. Through asynchronous processing, store-and-forward, and guaranteed delivery, it provides high availabilit y capabilities to keep business applications in continuous operation with uninterrupted service. It offers flexibility of integration by providing publish-and-subscribe and point-to-point functionality. Through location transparency and administrative control, it allows for a robust, service-based architecture. And most importantly, it is extremely easy to learn and use. In the next chapter we will take a look at how simple it is by building our first JMS application.
