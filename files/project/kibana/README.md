# kibana 使用简介
## 访问地址及账号
- 访问地址：[http://101.201.153.46](http://101.201.153.46)
- 查询账号： viewlog
- 查询密码： viewlog
### [登陆界面](http://101.201.153.46)
<img src="attachment/images/kibana01.png" width = "700" height = "300" alt="登陆页面" align=center />

## 现接入日志状况

索引名称 | 日志内容
:--- | :---
logstash-api.* | api  nginx访问日志
logstash-api-antispam* | api  antispam应用日志
logstash-app-m* | m站 应用日志
logstash-app-pc* | pc站 应用日志
logstash-app-shequ* | 社区 应用日志
logstash-app-rpc* | rpc程序应用日志
logstash-error-api* | api   nginx错误日志
logstash-error-m* | m站   nginx错误日志
logstash-error-pc* | PC站   nginx错误日志
logstash-error-shequ* | 社区   nginx错误日志
logstash-m* | m站  nginx访问日志
logstash-pc* | pc站  nginx访问日志
logstash-shequ* | 社区  ngixn访问日志
logstash-cms* | cms  nginx访问日志
logstash-rpc* | rpc 请求日志
logstash-varnish* | varnish 访问日志

## 使用方法
### 日志内容查看
<img src="attachment/images/kibana02.png" width = "700" height = "300" alt="登陆页面" align=center />

    使用者可自定义查看日志的时间间隔和刷新频率

<img src="attachment/images/kibana03.png" width = "700" height = "300" alt="登陆页面" align=center />

<img src="attachment/images/kibana04.png" width = "700" height = "300" alt="定义刷新频率" align=center />

    默认是查看接入日志的所有字段，用户可根据自己需求自定义查看字段范围

<img src="attachment/images/kibana05.png" width = "700" height = "300" alt="定义刷新频率" align=center />

    可以通过按钮直接添加过滤条件

<img src="attachment/images/kibana06.png" width = "700" height = "300" alt="定义刷新频率" align=center />

<img src="attachment/images/kibana07.png" width = "700" height = "300" alt="定义刷新频率" align=center />

    锁定要查询的日志内容后，可以根据需求，自定义过滤规则 

<img src="attachment/images/kibana08.png" width = "700" height = "300" alt="定义刷新频率" align=center />
   
[使用的lucene查询语法](https://segmentfault.com/a/1190000002972420)

    关键字检索：使用双引号包起来作为一个关键字搜索
        例：“shequ”
    字段检索：使用页面左侧显示的Available Fields中的字段搜索
        例：status:302
    范围搜索：数值和时间类型可对某一范围进行查询
        例: status:[400 TO 499]
            status:{400 TO 499}
            [ ] 表示端点数值包含在范围内，{ } 表示端点数值不包含在范围内
    通配符：
        ? 匹配单个字符
        * 匹配0到多个字符
    逻辑操作：AND  OR
    特殊字符需要转义：查询下面字符时需要使用 \ 进行转义
    + - && || ! () {} [] ^" ~ * ? : \

### 图形化展示
    日志信息图形化的配置权限，未对viewlog用户开放（为防止管理混乱）
    目前只针对nginx访问日志的信息进行了图形化配置，错误日志和应用日志暂时未进行相关处理，如有需求，可向运维部提出配置申请。

<img src="attachment/images/kibana09.png" width = "700" height = "300" alt="定义刷新频率" align=center />

<img src="attachment/images/kibana10.png" width = "700" height = "300" alt="定义刷新频率" align=center />
