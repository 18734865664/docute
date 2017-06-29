# 反垃圾项目

## 简介 
> 通过接入"网易易盾" 支持反垃圾，支持文本，图片两种形式

易盾官网：http://dun.163.com/

开发文档： [手册](https://www.163yun.com/docs/product/antispam/%E6%96%B0%E6%89%8B%E6%8C%87%E5%8D%97)

通过RPC服务对外提供服务，见[服务化](/project/soa/)

## 使用方法

在各个应用通过通过集成[client类库](/project/soa/?id=client%E7%AB%AF%E4%BD%BF%E7%94%A8)，实现服务的调用

## client代码结构

通过composer下载完代码后，进入/vendor/juzi/RPCClient中

## 注意
参见test/test_antispam.php示例程序集成到自己的应用中。composer代码库是不允许在本地修改的。否则会造成无法升级兼容

> 注意⚠️

1. 配置 $config需要根据情况修改，并按照规则写到config中
1. 注释中 //Todo 注明需要写日志的地方，建议写日志，记录taskID，便于需要时与"网易易盾"核对
1. 参数格式完全参照"网易易盾"规则 [详见](https://www.163yun.com/docs/product/antispam/%E8%A7%84%E8%8C%83%E8%AF%B4%E6%98%8E)
