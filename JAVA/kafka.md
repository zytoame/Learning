1. producer：生产者将数据发布到topic中，生成者将记录分配到topic的分区partition中，可以使用多个partition循环发送来实现多个server负载均衡
2. broker：日志的分区partition分布在Kafka集群的服务器上，每个服务器处理数据和请求时分享这些分区。，每个分区都会在已配置的服务器上进行备份确保容错性。broker都有leader和follows。leader server处理一切对分区的读写请求，follows只被动同步leader上的数据。当leader宕机了，followers中的一台server会自动成为新的leader。
3. Consumer：消费者使用group名称来表示，发布到topic中的每条记录将被分配到订阅消费组中的其中一个消费者实例。消费者实例可以分布在多个进程中或多个机器上
	1. 所有消费者实例在同一个消费组，消息记录会负载均衡到消费组中的每一个消费者实例
	2. 在不同消费组中，则每条消息记录广播到所有消费组或消费者进程中

- 生产者流程
	- 主线程producer经过拦截器，序列化其，分区器，将处理好的消息发送到消息累加器中
	- 消息累加器每个分区对应一个队列，收到消息放入队列
	- 使用producerBatch批量进行消息发送到sender线程处理（为了提高发送效率，减少带宽），ProducerBatch中就是我们需要发送 的消息。消息累加器中可以使用Buffer.memory配置，默认为32MB
	- Sender线程从队列头部开始读取消息，创建Request后被缓存，提交到Selector，Selector发送消息到Kafka集群
	- 还没有收到Kafka集群ack响应的消息会将未响应接受消息的请求进行缓存，
	- 当收到Kafka集群ack响应后，会将Request请求在缓存中清除并同时移除消息累加器中的消息
- 消费者流程
	- 消费组中的消费者向各自注册的分区上进行消费消息
	- 消费者消费消息后会将当前标注的消费位移信息以消息的方式提交到位移主题中记录，一个消费组中的多个消费者会做负载均衡，如果一个消费者宕机会自动切换到组内别的消费者进行消费
		- 组内多个消费者可以公用一个ConsumerID，

- 消息传递语义
	- 最多发送一次：造成数据丢失
	- 至少发送一次：数据重复消费
	- 只发送一次：我们想要的效果
		- 需要满足
			- 生产者发布消息的持久性保证
			- 消费者使用消息的循序性保证
		- 期间可能出现的现象
			- 生产者和消费者可能挂掉
			- 多个消费者消费情况
			- 生产者写入磁盘的数据可能丢失
- 生产者发送消息
	- 发布的消息被提交，且有一个副本分区的broker处于活动状态，消息就不会丢失
	- 遇到网络错误，无法确定错误是在消息提交前还是之后发生的
		- 0.11.0.0版本之前，Kafka至少发送一次语义会造成消息重复发布
		- 之后，Kafka支持幂等传递选项，保证重新发送不会导致日志中的重复条目。
			- 代理为每一个生产者分配一个ID，使用生产者与每条消息一起发送的序列号对消息进行重复删除。
			- 生产者使用类似事务的语义学将消息发送到多个主题分区的能力，要么所有消息都成功写入，要么没有消息
	- ack
		- 0：生产者不会等待服务器的确认。记录将立即添加到套接字缓冲区并视为已发送。不会重试，每条记录的偏移量始终设置为-1
		- 1：leader将等待整套同步副本确认记录。保证了只要至少有一个同步副本仍然有效，记录就不会丢失。
- 消费者
	- 所有副本都有完全相同的日志，相同的偏移量。消费者维护偏移量。
	- 消费者崩溃，topic分区需要被另一个消费者接管
		- 消费者逻辑先处理消息再更新偏移量。更新偏移量之前消息处理成功后挂掉，下一个消费者接替消费时造成重复消费。对应“至少一次”
		- 先更新偏移量，在处理消息。处理消息之前，更新偏移量之后挂掉，下一个消费组接替消息时造成消息丢失。对应“最多一次”
	- 解决：将更新偏移量和处理消息放在一个事务中
[深入解析 Kafka Exactly Once 语义设计 & 实现-阿里云开发者社区](https://developer.aliyun.com/article/1172598)
[美团面试：对比分析 RocketMQ、Kafka、RabbitMQ 三大MQ常见问题？-阿里云开发者社区](https://developer.aliyun.com/article/1662976?scm=20140722.ID_community%40%40article%40%401662976._.ID_community%40%40article%40%401662976-OR_rec-PAR1_0b1639b517587640135518272e3ab2-V_1-RL_community%40%40article%40%401554126)
[Kafka-设计思想-2_kafka至少一次-CSDN博客](https://blog.csdn.net/lu070828/article/details/142883549)
### 启动ZooKeeper

Kafka使用ZooKeeper来维护集群元数据，因此需要先启动ZooKeeper：

```bash
sudo /usr/local/kafka/bin/zookeeper-server-start.sh /usr/local/kafka/config/zookeeper.properties
```

### 7. 启动Kafka服务

```bash
sudo /usr/local/kafka/bin/kafka-server-start.sh /usr/local/kafka/config/server.properties
```

这将在后台启动Kafka服务。

### 8. 创建Kafka Topic

使用以下命令创建一个Kafka Topic：

```bash
kafka-topics.sh --create --topic test-topic --zookeeper localhost:2181 --partitions 1 --replication-factor 1
```

### 9. 验证Kafka和Topic

使用以下命令列出所有的Kafka Topics：

```bash
kafka-topics.sh --list --zookeeper localhost:2181
```

### 10. 停止Kafka和ZooKeeper

当你完成测试后，可以使用以下命令停止Kafka和ZooKeeper服务：

```bash
sudo /usr/local/kafka/bin/kafka-server-stop.sh
sudo /usr/local/kafka/bin/zookeeper-server-stop.sh
```