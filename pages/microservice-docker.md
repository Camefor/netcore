# 微服务容器化实践

## 1. 微服务架构实践
Nginx放在什么位置？
负载均衡 -> 网关集群 -> 注册中心集群 -> 应用服务集群 -> 数据库服务
Docker容器化后的微服务如何通讯？
使用SingalR后如何反推消息