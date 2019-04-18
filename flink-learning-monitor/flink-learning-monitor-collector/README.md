## Flink 监控数据采集

因为数据采集是非常重要的，如果在底层数据采集的过程中就断了，那么后面的存储和告警链路将全部失效，所以为了保证后面链路的可用性，
数据采集的话就不能也是一个 Flink Job，否则因为 Flink 挂了的话，那么就会导致数据采集的 Job 失效，导致整个监控告警链路失效。

另外，也不符合 Flink 的特点，Flink 其实更在于计算，有数据源（source）和下发处（sink），这里我们采集数据的话就自己写一个项目利用
Flink 自己暴露的 Rest API 去采集相关数据（JobManager、TaskManager、Job 等），将采集好的数据组织好成一个个 Metrics，然后发送到 Kafka。