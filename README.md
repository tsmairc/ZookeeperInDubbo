# 学习zookeeper注册中心原理
* 1.zookeeper的数据结构是一个树如下图所示，zookeeper的作用是维护这个树。
![](https://github.com/tsmairc/ZookeeperInDubbo/blob/master/image/image1.png?raw=true)

* 2.zookeeper连接分两种，一种是临时节点，一种是永久节点，dubbo连接zookeeper是用了临时节点。用了临时节点，这时会有一个session保持连接状态，当dubbo断开连接时，session会撤消，这时dubbo在zookeeper上生成的节点也会被删除。
![](https://github.com/tsmairc/ZookeeperInDubbo/blob/master/image/image3.png?raw=true)

### dubbo在zookeeper中生成的节点如下图所示
![](https://github.com/tsmairc/ZookeeperInDubbo/blob/master/image/image2.png?raw=true)
<br/>上面中，叶子节点代表不同dubbo服务器，当dubbo服务器断开时，zookeeper也会把属于当前dubbo服务器的叶子节点删除，zookeeper设计就是一个观察者模式，dubbo的消费者会监听这些叶子节点，通过获取这些叶子结点去访问提供者
![](https://github.com/tsmairc/ZookeeperInDubbo/blob/master/image/image4.png?raw=true)

![参考信息](https://www.ibm.com/developerworks/cn/opensource/os-cn-zookeeper/)

