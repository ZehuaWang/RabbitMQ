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

