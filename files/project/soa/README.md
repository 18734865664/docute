# 服务化项目

## 提供服务列表

服务名 | 调用 | 备注 | ...
---|---|---
反垃圾 | App\Antispam::check | 文本反垃圾，图片反垃圾 | [more](/project/antispam/)

## 服务方案
方案服务端，客户端完全基于Swoole实现RPC通讯
> 参考:  [基于swoole的RPC方案](https://wiki.swoole.com/wiki/page/683.html) 不过文档又老，又不完善

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
基于Swoole框架中rpc client类，通过[composer](/technology/php/composer)管理

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
> git:ssh://[username]@111.203.201.131:8022/var/www/juzi-php-vendor-rpcclient.git

目录结构介绍
```
|-src                           // 是本程序源代码目录
    |-Swoolelib                 // 从Swoole框架下抽出来的代码，除了修改namespace外，为了以后便于升级也不应做任何其他修改。
    |-JuziRpcClient             // rpcclient端集成代码，
        |-Exception             // 自定义异常处理class
            |-InvalidParam.php  // 参数无效异常
            |-RpcSystem.php     // Client在与RPC服务端链接过程中返回的系统级异常，如IP拒绝访问，验证失败等
            |-RpcService.php    // Client在调用具体RPC服务是，服务本身返回的异常，如易盾调用失败，传递参数不对
        |-Antispam.php          // 反垃圾服务client端集成代码
        |-Base.php              // 各个client端程序接口类，新加入的服务client程序需要实现此interface的函数
        |-RpcClient.php         // 封装处理rpc调用的class，主要开发集中在这里
    |-lib_config.php            // 仅为test下test.php加载swoolelib类库使用
|-test                          // 是示例demo程序    
    |-test_antispam.php         // 示例测试demo
    |-composer.json.default     // 在各个应用的根目录下composer.json文件加入本文件示例内容。
```

### 步骤
1. \# mkdir script 
1. \# curl -sS https://getcomposer.org/installer | php -- --install-dir=script
1. 修改根下composer.json,加入rpcclient
1. \# /data/php/bin/php script/composer.phar update
1. require_once vendor/autoload.php文件
1. 使用方法，见composer中示例test目录下，参照示例程序在应用中集成。

> 注意⚠️

1. ⚠️请注意，**不允许在下载下来的composer代码直接修改**。composer做为代码库是**单独维护升级**。
1. 修改composer.json,请参见test下composer.json.default文件
1. /test/test.php 是示例程序
1. /test/composer.json.default 是接入项目的composer.json中接入本插件的示例

