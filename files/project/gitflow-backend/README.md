# GIT工作流程
## 通用工作流

 - ![image](attachment/images/GIT工作流1.png)
 - 适用于API、社区、PC站、M站等
### 分支说明
 - Master `主分支、受保护分支、管理员可操作`

  > 存放随时可供在生产环境中部署的代码。当项目开发结束并结测，产生了一份新的可供部署的代码时，Master分支上的代码会被更新。同时每一次上线添加对应的版本号标签（TAG）
 
 - Develop `主分支、受保护分支、管理员可操作`

  > 保存当前最新开发成果的分支
  
  - Feature  `辅助分支`

  > 通常是在开发一项新的功能时使用，从Develop分支派生而来、最终合并回Develop分支或者干脆被抛弃掉。
  
  - Release  `辅助分支、管理员可操作`

  > 为发布新的产品版本而设计, 对应某个版本的测试阶段。从Develop分支派生、上线时合并到Master分支&Develop分支，并销毁。

  - Bugfix  `辅助分支`

  > 用于修复Release分支的Bug, 从Release分支派生而来、并将被合并回Release分支。

  - Hotfix  `辅助分支`

  > 当生产环境中发现了严重到必须立即修复的软件缺陷时，就需要从Master分支上指定的TAG版本派生Hotfix分支来组织代码的紧急修复工作

 ### 分支命名规则
 
  - Feature分支 `fetcher/{版本}-{功能}`
  > 如: feature/v4.1-flash_news(V4.1快讯功能)
  - Release分支 `release/{版本}`
  > 如: release/v4.1
  - Bugfix分支  `bugfix/{版本}-{时间}-{开发者}-[功能]`
  > 如: bugfix/v4.1-170909-wxp-flash_news
  > bugfix/v4.1-170909-wxp
  - Hotfix分支 `hotfix/{版本}-{时间}-{开发者}-{功能}`
  > 如: hotfix/v4.1-170909-wxp-flash_news

## 多版本并行工作流

 - ![image](attachment/images/GIT工作流2.png)
 - 适用于CMS等
### 说明
 - Develop根据分支并行情况拆分为多个主干分支。
 > 如CMS拆分为develop-app & delelop-web
 - Release分支从相应的Develop分支派生而来，可对应多个测试环境。
 - Release分支上线时，除了合并到master分支外、需要同时合并到多个Develop分支。
 - Hotfix分支上线时，除了合并到master分支外、同样需要合并到多个Develop分支。
 - Feature分支从对应的Develop分支派生而来、并将合并回对应的Develop分支。
 - Bugfix分支从对应的Release分支派生而来、并将合并回对应的Release分支。
