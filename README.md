# RabbitMQ
分布式系统-消息中间件

## 消息中间件概述

MQ全称为Message Queue 消息队列是应用程序和应用程序之间的通信方法

为什么使用MQ

在项目中 可以将一些无需及时返回且耗时的操作提取出来,进行异步处理

这种处理的方式大大节省了服务器的请求响应的时间 从而提高了系统的吞吐量

开发消息队列通常有以下的应用场景:

1. 任务异步处理 
将不需要同步处理且耗时的操作由消息队列通知消息接收方进行异步处理. 提高应用程序的响应时间

2. 应用程序解耦合
MQ 相当于一个中介 生产方通过MQ与消费方交互

3. 销峰填谷
订单系统 在下订单时会向数据库中写数据. 但是数据库只能支持1000左右的并发写入. 并发量在高容易宕机. 低并发时也就100多个, 但是在高峰的时候 并发达到5000+

消息可以被MQ保存起来 然后系统就可以按照自己的消费能力消费. 比如每秒1000个数据
这样慢慢写入数据库就不会卡死

![image](https://user-images.githubusercontent.com/40006814/158725819-b3011929-1997-4ea8-a039-3384c214e365.png)

但是使用了MQ之后 限制消消息的速度为 1000 但是这样一来 高峰期产生的数据势必会被挤压在MQ中 高峰就被削掉了, 但是因为消息积压 在高峰期过后的一段时间内 消费消息的速度维持在1000 直到消费完积压的消息 这就叫填谷.

## AMQP(高级消息队列协议) 和 JMS

MQ是消息通信的模型; 实现MQ的两种主流方式: AMQP JMS

AMQP 是一种协议 更准确的说是一种 binary wire-level protocol (链接协议). 这是其和JMS的本质区别. AMQP不从API层进行限定 而是直接定义网络交换的数据格式

JMS JMS就是Java 消息服务 应用程序接口. 是一个Java平台中关于面向消息中间件(MOM)的API 用于在两个程序之间 或分布式系统中发送消息 进行异步通信

AMQP与JMS的区别

JSM是定义了统一的接口 来对消息操作进行统一; AMQP是通过规定协议来统一数据交互的格式

JMS限定了必须使用Java语言; AMQP只是协议 不规定实现方式 所以是夸语言的

JMS贵定了两种消息模式 而AMQO的消息模式更加丰富

消息队列产品:

ActiveMQ 基于JMS

RabbitMQ: 基于AMQP协议 erlang语言开发 稳定

RocketMQ: 基于JMS 阿里巴巴产品

Kafka: 类似MQ的产品 分布式消息系统 高吞吐量

RabbitMQ提供了6种模式: 简单模式 work模式 Publish/Subscribe发布与订阅模式 Routing路由模式 Topics主题模式 RPC远程调用模式 

## JMS 教程

JMS -> JMS API provides vernder independent access to Enterprise Messaging Systems Like JBoss Messaging, WebSphere MQ

BEW weblogic

JAVA Messaging Service has 2 models:

Point to Point Queues

Publish / Subscribe Topics

JMS Diagram

