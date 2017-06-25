# 帮助

## 如何开始

> git地址：ssh://[username]@[ip]:[port]/var/www/juzi-docute.git

> Server：内网192.168.10.70:8033

1. git clone 本文档项目代码
1. 在根目录下修改"index.html"设置导航。
1. 在"files文件夹"中进入要放置文件的文件夹。
1. 编写内容markdown文件。
1. 提交git
1. 到 服务器上 git pull代码，部署好。
1. 打开文档地址，查看最终结果

<p class="warning">
  如果您对所创建的内容暂时不知道归档到哪里的话，可以先放置在"[暂存处](/temp/)"。后期可以讨论统一规划<br>
</p>

## 顶部导航
根目录下index.html文件中

[参考](https://docute.js.org/#/zh-Hans/?id=%E5%AF%BC%E8%88%AA%E6%A0%8F)

例如：
````
<script>
    docute.init({
        url : "/files/",
        nav: [
            // 首页
            {title: '首页', path: '/'},
            {title:"项目",type:"dropdown",items:[
                {title:"服务化",path:"/project/soa/"},
                {title:"直播",path:"/project/live/"},
                {title:"反垃圾",path:"/project/antispam/"}
            ]},
    });
</script>
````

## 左侧导航
[参考](https://docute.js.org/#/zh-Hans/?id=%E4%BE%A7%E8%BE%B9%E6%A0%8F)

侧边栏的目录表 (table of contents) 是从你的 markdown 文件解析来的


## 默认文件

每个文件夹下README.md是该路径下的默认访问文件


## 相关
> git clone下git库juzi-docute.git，编辑文件(markdown语法)，修改完成后提交git，Server上git pull。则部署完毕。

主要目录结构：
- attachment （所有附件放在这里面）
- dist （静态资源，js，css等放在这里面）
- files （.md文件 - ⚠️主要在这里操作）
- index.html (入口文件，⚠️导航，配置等在这里修改)



> 语法：[markdown](http://www.appinn.com/markdown/)

> markdown编辑器：[有道云笔记](http://note.youdao.com/)，[Mou](http://25.io/mou/)，[phpstorm](http://www.jetbrains.com/phpstorm/)

> 参考：[Docute](https://docute.js.org/#/home)
