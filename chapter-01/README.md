# 创建 ORM 引擎

所有操作均需要事先创建并配置 ORM 引擎才可以进行。XORM支持两种 ORM 引擎，即 Engine 引擎和 Engine Group 引擎。一个 Engine 引擎用于对单个数据库进行操作，一个 Engine Group 引擎用于对读写分离的数据库或者负载均衡的数据库进行操作。Engine 引擎和 EngineGroup 引擎的API基本相同，所有适用于 Engine 的API基本上都适用于 EngineGroup，并且可以比较容易的从 Engine 引擎迁移到 EngineGroup引擎。