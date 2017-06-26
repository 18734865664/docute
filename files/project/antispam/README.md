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

目录结构介绍
```
|-src                       // 是本程序源代码目录
    |-swoolelib             // 从Swoole框架下抽出来的代码，除了修改namespace外，为了以后便于升级也不应做任何其他修改。
    |-lib_config.php        // 仅为test下test.php加载swoolelib类库使用
    |-rpcclient.php         // 封装处理rpc调用的class，主要开发集中在这里
|-test                      // 是示例demo程序    
    |-test.php              // 示例demo
    |-composer.json.default // 在各个应用的根目录下composer.json文件加入本文件示例内容。
```

## 注意
参见test.php示例程序
```
$rpc = new JuziRpcClient\rpclient($config);
```  
$config需要根据情况修改

注释中 //Todo 注明需要写日志的地方，建议写日志，记录taskID，便于需要时与"网易易盾"核对

```
$result = $this->rpc_client("App\\Antispam::check", ['online_text', $params]);
```
传递的参数中
'online_text' 为检测类型，支持
1. online_text      实时检测文本
1. online_img       实时检测图片
1. callback_text    离线检测文本
1. callback_img     离线检测图片

$params为具体提交的需要检测的内容

参数格式完全参照"网易易盾"规则 [详见](https://www.163yun.com/docs/product/antispam/%E8%A7%84%E8%8C%83%E8%AF%B4%E6%98%8E)
