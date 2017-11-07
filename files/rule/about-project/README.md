![image](http://cdn.happyjuzi.com/juzi-pc/pc1.6.2/img/new_logo.png)
### 项目简介
【简单介绍下本项目，如：本库是橘子娱乐app的接口API代码库】

### 目录结构说明
【以下为api-juzi示例】

```
├── service.sh  // 启动脚本,参数:start|stop|restart|reload
├── app_server.php // 入口文件
├── apps
    ├── activity    // app的不定时活动
    ├── advertise   // 广告
    ├── applet      // 橘子娱乐小程序,代码已移植,待废弃
    ├── classes     // 基类代码
    ├── cooperation     // 合作项目代码,以后的合作项目要放在本目录
    ├── explore     // 橘子娱乐app发现版,已移植到主版本,待废弃
    ├── foundpage       // 旧版本发现功能,待废弃
    ├── juzi        //  橘子娱乐app主版本
    ├── nightpoison     // 深夜读物app,貌似已下线,待废弃
    ├── tasks       // 程序异步任务,主要用于图片上传功能,反馈|用户头像|明星留言
    ├── v2.X        // 橘子娱乐历史版本app 包括1.0、2.0～2.10
    ├── wapsite // 旧版的m站,待废弃
    ├── watch       // 合作项目-三星手表
    └── weather     // 合作项目-墨迹天气
├── cache  // 暂未用
├── config  //  存放所有配置文件的目录
    ├── common.php  //  公共配置
    ├── rewrite.php //  项目所有路由配置
    ├── status.php  //  环境设定    dev|test|prod
    ├── ...
├── cron    // 定时任务存放目录
├── libs    // 类库
├── log     // 日志目录 
├── script  // 初始脚本存放目录
├── static  // 文件缓存存放目录
    ├── content // 文章的content文件缓存目录,取自 juzi_content表
    └── page
       ├── v4.1    // 文章的各个版本json文件缓存目录
       └── ...
├── swagger // swagger配置
├── upload  // 上传
└── composer.json
└── vendor  
```

### 部署说明

#### 环境要求
【如php版本及扩展以及其他的一些依赖说明】
`php7.1`
`openssl.so` `protobuf.so` `redis.so` `solr.so`     `swoole.so`

#### 配置
【配置文件所需要修改的地方罗列，目录需要，以及目录权限需要等】

#### 启动服务
【如：命令行执行`sh service.sh start ` or ` php app_server.php`，如若没有，请省略该项】
#### 停止服务
【如：`Ctrl+C`，如若没有，请省略该项】
#### 使用说明
【如果是类库介绍下使用方法；如果是服务，介绍下调用方式】
