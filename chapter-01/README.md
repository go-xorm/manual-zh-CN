# 创建 ORM 引擎

所有操作均需要事先创建并配置 ORM 引擎才可以进行。XORM支持两种 ORM 引擎，即 Engine 引擎和 Engine Group 引擎。一个 Engine 引擎用于对单个数据库进行操作，一个 Engine Group 引擎用于对读写分离的数据库或者负载均衡的数据库进行操作。