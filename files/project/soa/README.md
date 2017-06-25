# 服务化项目

## 服务方案
方案服务端，客户端完全基于Swoole实现RPC通讯
> 参考:  [基于swoole的RPC方案](https://wiki.swoole.com/wiki/page/683.html) 不过文档很不完善

### 服务端
> git:ssh://[username]@111.203.201.131:8022/var/www/juzi-rpc.git

### 客户端
> git:ssh://[username]@111.203.201.131:8022/var/www/juzi-rpc-client.git


### 架构图
![image](attachment/images/soajiagou.png)

### 提供服务列表

服务名 | class | 入口func | 备注 
---|---|---|---
反垃圾 | App\Antispam | check | 文本反垃圾，图片反垃圾

