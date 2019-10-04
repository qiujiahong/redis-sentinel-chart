# REDIS哨兵chart 


## 简介

* 本chart安装一个redis哨兵集群，可提供给集群的其他应用使用；
* 集群模式： 1主2从，3哨兵
* 哨兵连接信息： 
  * redis-sen-0.redis-sen 26379
  * redis-sen-1.redis-sen 26379
  * redis-sen-2.redis-sen 26379
  * 默认密码: 123456

## 可配置参数

```YAML
redis:
  # redis 端口
  port: 6379
  # redis 哨兵端口
  sentinelPort: 26379
  # redis master 访问免密
  password: 123456
```
## 安装与卸载

```bash
# 避免重复安装最好指定名字
helm install --name redis-sen ./
# 配置参数
helm install --name redis-sen --set redis.port=6479 ./
# 卸载
helm delete redis-sen 
helm del --purge redis-sen
```

## 测试命令: 

```bash
# 进入其中一个pod节点
kubectl exec -it redis-sen-0 bash 
# 登录redis哨兵
redis-cli -h redis-sen-1.redis-sen -p 26379
# 输入命令查看集群信息
info 
```

> 如果不再同一个namespace下，可以使用完整域名，如：``redis-sen-0.redis-sen.default.svc.cluster.local``


## 使用到的镜像

该chart使用了docker hub官方的redis镜像-redis:5.0.6-buster，如果网络条件良好，读者可以自行获取。否则可科学上网。