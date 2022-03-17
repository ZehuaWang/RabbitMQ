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

但是使用了MQ之后 限制消消息的速度为1
