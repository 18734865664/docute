# composer使用
参考：[http://docs.phpcomposer.com/](http://docs.phpcomposer.com/)


## 基本使用
### 安装
通过 --install-dir 选项指定 Composer 的安装目录
> curl -sS https://getcomposer.org/installer | php -- --install-dir=bin


```
curl -sS https://getcomposer.org/installer | php -- --install-dir=script
```


### 使用
要解决和下载依赖
> php composer.phar install


```
/data/php/bin/php script/composer.phar install
```
### 自动加载
Composer 还准备了一个自动加载文件，它可以加载 Composer 下载的库中所有的类文件。使用它，你只需要将下面这行代码添加到你项目的引导文件中
``` 
require 'vendor/autoload.php';
```
### composer.lock文件
在安装依赖后，Composer 将把安装时确切的版本号列表写入 composer.lock 文件。这将锁定改项目的特定版本。

**⚠️请提交你应用程序的 composer.lock （包括 composer.json）到你的版本库中**

这是非常重要的，因为 install 命令将会检查锁文件是否存在，如果存在，它将下载指定的版本（忽略 composer.json 文件中的定义）。

这意味着，任何人建立项目都将下载与指定版本完全相同的依赖。你的持续集成服务器、生产环境、你团队中的其他开发人员、每件事、每个人都使用相同的依赖，从而减轻潜在的错误对部署的影响。即使你独自开发项目，在六个月内重新安装项目时，你也可以放心的继续工作，即使从那时起你的依赖已经发布了许多新的版本。

如果不存在 composer.lock 文件，Composer 将读取 composer.json 并创建锁文件。

这意味着如果你的依赖更新了新的版本，你将不会获得任何更新。此时要更新你的依赖版本请使用 update 命令。这将获取最新匹配的版本（根据你的 composer.json 文件）并将新版本更新进锁文件。


```
php composer.phar update
```

如果只想安装或更新一个依赖，你可以白名单它们：


```
php composer.phar update monolog/monolog [...]
```


## 库（资源包）
### 每一个项目都是一个包
一旦你有一个包含 composer.json 文件的库存储在线上版本控制系统（例如：Git），你的库就可以被 Composer 所安装

> composer.json文件中 classmap用于没有遵循psr-04规范的class文件用class引入

```
{
  "name": "juzi/RPCClient",
  "description": "rpc客户端程序，基于swoole",
  "keywords": ["rpc", "swoole"],
  "type": "library",
  "license": "MIT",
  "homepage": "http://happyjuzi.com",
  "support": {},
  "authors": [
    {
      "name": "Kevin",
      "email": "congjunwei@happyjuzi.com"
    }
  ],
  "require": {
    "php": "^5.5|^7.0"
  },
  "autoload": {
    "classmap": [
      "./src"
    ]
  }
}
```

其中autoload推荐使用psr-04标准,如下

```
    "autoload": {
        "psr-4": {
            "Monolog\\": "src/",
            "Vendor\\Namespace\\": ""
        }
    }
```
### 项目根目录下的composer.json文件

```
{
  "repositories": [
    {
      "type": "vcs",
      "url": "ssh://git@111.203.201.131:8022/var/www/juzi-php-vendor-rpcclient.git"
    }
  ],
  "require": {
    "juzi/RPCClient": "170622.x-dev"
  }
}

```
> ⚠️ "juzi/RPCClient"与库包中“name”一致

> ⚠️ 后面的版本号"170622.x-dev"，需要注意

如果是master分支，则为"dev-master"

如果是feature分支则为"[分支名].x-dev，x是技术要求，必须加composer才可以认

如果是标签tag则为"1.0.0",应该符合 'X.Y.Z' 或者 'vX.Y.Z' 的形式，-patch、-alpha、-beta 或 -RC 这些后缀是可选的

关于指定版本，[参考](http://docs.phpcomposer.com/02-libraries.html#Specifying-the-version)



## composer项目版本控制
使用git版本控制
> ssh://git@111.203.201.131:8022/var/www/juzi-php-vendor-rpcclient.git。
⚠️注意 使用ssh密钥登录

### git中怎么管理
如果你正在使用Git来管理你的项目， 
1. 你可能要添加 vendor 到你的 .gitignore 文件中。 你不会希望将所有的代码都添加到你的版本库中。
1. 提交/composer.json文件到git库中.
1. 提交/composer.lock文件到git库中。
1. 测试环境中，在"require"节点需要设置版本号
    1. 测试环境，设置为feature分支，如"170622.x-dev"。
    1. 正式环境，设置为master分支，如"dev-master"。


橘子composer项目版本库命名规范
> 库名：juzi-php-vendor-rpcclient.git。通过"-"号分隔，最后部分“如rpcclient”区分每个插件库名。

## 常用命令
> init

看到了如何手动创建 composer.json 文件。实际上还有一个 init 命令可以更容易的做到这一点。

当您运行该命令，它会以交互方式要求您填写一些信息，同时聪明的使用一些默认值。
> install

install 命令从当前目录读取 composer.json 文件，处理了依赖关系，并把其安装到 vendor 目录下。

> update

为了获取依赖的最新版本，并且升级 composer.lock 文件，你应该使用 update 命令。
> validate

在提交 composer.json 文件，和创建 tag 前，你应该始终运行 validate 命令。它将检测你的 composer.json 文件是否是有效的