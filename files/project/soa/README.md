# 服务化项目

## 提供服务列表

服务名 | class | 入口func | 备注 
---|---|---|---
反垃圾 | App\Antispam | check | 文本反垃圾，图片反垃圾

## 服务方案
方案服务端，客户端完全基于Swoole实现RPC通讯
> 参考:  [基于swoole的RPC方案](https://wiki.swoole.com/wiki/page/683.html) 不过文档很不完善

### 服务端
基于Swoole框架，主要目录结构
```
\
|-apps                      \\应用文件
    |-classes               \\RPC服务文件存放处
        |-Antispam.php      \\RPC服务类
        |-...
    |-controllers           \\controller文件存放位置，仅用于测试程序或示例
        |-Testantispam.php  \\反垃圾测试示例程序
        |-...
|-cache                     \\存放缓存
|-config                    \\配置文件
    |-common.php            \\基本配置
    |-level.php             \\服务降级配置
    |-log.php               \\日志配置
    |-status.php            \\运行模式，debug模式，守护进程模式配置
|-log                       \\存放日志
|-script                    \\存放执行脚本
|-upload                    \\存放上传文件
|-rpc_server.php            \\启动服务文件

```
### 客户端
基于Swoole框架中rpc client类，通过[composer](technology/php/composer)管理

### 架构图
![image](attachment/images/soajiagou.png)

## Server端部署
> git:ssh://[username]@111.203.201.131:8022/var/www/juzi-rpc.git

### 步骤
1. git clone git:ssh://[username]@111.203.201.131:8022/var/www/juzi-rpc.git
1. 修改config目录中status.php，运行模式，debug模式，守护模式
1. /path/php rpc_server.php start启动

### 启动/停止/重加载
```
php rpc_server.php start|stop|reload
```


## client端使用
> git:ssh://[username]@111.203.201.131:8022/var/www/juzi-rpc-client.git
