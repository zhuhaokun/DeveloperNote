# 查看redis进程
```bash
ps aux | grep redis
```
# 启动redis
```bash
bin/redis-server 7001/redis.conf
```
# 登录
```bash
redis-cli -h 186.1.62.230 -p 7001 -a gzbredis@123
```
# 创建redis集群
```bash
redis-cli --cluster create --cluster-replicas 1   186.1.62.230:7001 186.1.62.230:7002 186.1.62.231:7001 186.1.62.231:7002 186.1.62.232:7001 186.1.62.232:7002 -a gzbredis@123
```
# 查看集群状态
```bash
redis-cli --cluster check 186.1.62.230:7001 -a gzbredis@123
```
# 查看节点信息
```bash
redis-cli -h 186.1.62.230 -p 7001 -a gzbredis@123 cluster nodes    
```

