# gitlab使用手册

## 访问地址/账号申请
### gitlab 访问链接：  
1. 内网访问：[http://192.168.10.154:7001](http://192.168.10.154:7001)  
2. 外网访问：[http://111.203.201.138:7001](http://111.203.201.138:7001)

### 账号申请：
1. 自助申请：  
   > 在登陆页面，选择注册

   <img src="attachment/images/gitlab/gitlab_注册.png" width = "800" height = "400" alt="注册页面" align=center />
2. 用户邀请：  
   > 登陆后：选择 群组 --> 成员 ---> 添加成员   

   <img src="attachment/images/gitlab/成员邀请.png" width = "800" height = "400" alt="邀请用户" align=center />

3. 管理员添加：  
   > 管理员用户登录：管理区域 ---> 新建用户

```
需要向管理员提供：姓名，用户名，电子邮箱
```
   <img src="attachment/images/gitlab/新建用户.png" width = "800" height = "400" alt = "新建用户" align = center />

## 使用简介
### 新建项目:   
   > 登录成功后，点击导航条上的 “+” 就可以进入创建项目的页面

<img src="attachment/images/gitlab/新建项目1.png" width = "800" heigth = "400" alt = "新建项目1" align = center />  
（1）Project path：项目的路径，一般可以认为是项目的名称

（2）Import prject from：从哪导入项目，提供Github/Bitbucket等几个选项

（3）Description（项目的描述）：可选项，对项目的简单描述

（4）Visibility Level（项目可见级别）：提供Private（私有的，只有你自己或者组内的成员能访问）/Internal（所有登录的用户）/Public(公开的，所有人都可以访问)三种选项。
### 项目导入
1. 自动导入
    > 新建项目时，导入项目处选择要导入项目的源地址
   
    <img src="attachment/images/gitlab/新建项目2.png" width = "800" heigth = "400" alt = "新建项目2" align = center />  
    <img src="attachment/images/gitlab/新建项目3.png" width = "800" heigth = "400" alt = "新建项目3" align = center />  
2. 手动导入(以test项目为例)
    > 创建一个空项目，然后手动导入项目

    a. Git 全局设置
    ```
    git config --global user.name "Administrator"
    git config --global user.email "admin@example.com"
    ```  
    b. 创建新版本库  
    
    ```
    git clone ssh://git@111.203.201.138:36588/root/test.git
    cd test
    touch README.md
    git add README.md
    git commit -m "add README"
    git push -u origin master
    ```
    c. 已存在的文件夹  
    ```
    cd existing_folder
    git init
    git remote add origin ssh://git@111.203.201.138:36588/root/test.git
    git add .
    git commit -m "Initial commit"
    git push -u origin master
    ```  
    d. 已存在的 Git 版本库  
    ```
    cd existing_repo
    git remote add origin ssh://git@111.203.201.138:36588/root/test.git
    git push -u origin --all
    git push -u origin --tags
    ```
### 群组管理
    > 实现多人协作及权限分组管理
    
1. 新建群组  
    a. 项目默认分组
    ```
    新建项目时，如果没有选择分组，会生成一个与项目名同名的群组，群组成员默认有项目创建者
    ```
    <img src="attachment/images/gitlab/同名群组.png" width = "800" heigth = "400" alt = "同名群组" align = center />
    b. 创建特定分组  
    1. 点击导航条上的 “+” 就可以进入创建群组的页面
    2. 点击 群组 ---> New group
    <img src="attachment/images/gitlab/新建群组.png" width = "800" heigth = "400" alt = "新建群组" align = center />
2. 成员管理  
    > 管理界面： 群组 ---> 指定群组 ---> 成员  
                  > 项目 ---> 指定项目 ---> 设置 ---> 成员 

    a. 添加/邀请成员  
    > 添加现有用户进群组，或者邀请新用户注册并加入到群组

    <img src="attachment/images/gitlab/添加成员.png" width = "800" heigth = "400" alt = "添加成员" align = center />
    [群组角色具体权限](http://192.168.10.154:7001/help/user/permissions)
    
### 问题管理（工作流）
    > 工作流管理

1. 新建问题（任务）
    > 管理界面：项目 ---> 指定项目 ---> 问题 ---> 新建问题

    <img src="attachment/images/gitlab/新建问题.png" width = "800" heigth = "400" alt = "新建问题" align = center />
    <img src="attachment/images/gitlab/新建问题2.png" width = "800" heigth = "400" alt = "新建问题2" align = center />
    <img src="attachment/images/gitlab/新建问题3.png" width = "800" heigth = "400" alt = "新建问题3" align = center />
2. 查看问题
    > 查看已创建的问题状态（未关闭/已关闭）

    <img src="attachment/images/gitlab/问题查看.png" width = "800" heigth = "400" alt = "问题查看" align = center />
3. 任务看板
    > 可以直观地管理工作流,默认看板中有：Backlog/To Do/Doing/Closed 栏目

    **新增的任务，会出现在看板中的 Backlog 栏**
    <img src="attachment/images/gitlab/任务看板1.png" width = "800" heigth = "400" alt = "任务看板" align = center />

    **被指派的问题责任人，登陆后在待办事项中，可以看到任务指派记录**
    <img src="attachment/images/gitlab/待办事项.png" width = "800" heigth = "400" alt= "待办事项" align =center />

    **被指派人，在任务管理栏中，将问题移动到To Do 或Doing**
    <img src="attachment/images/gitlab/任务看板2.png" width = "800" heigth = "400" alt = "任务看板" align = center />

    **工作结束后，将问题移动到Closed，关闭问题**
    <img src="attachment/images/gitlab/任务看板3.png" width = "800" heigth = "400" alt = "任务看板" align = center />
## 权限安全
### 添加配置SSH公钥
将ssh公钥配置到gitlab，一边我们通过ssh协议访问Git仓库
1. 生成公钥：  
    a. linux 系统
    ```
    ssh-keygen  -t rsa #一路回车
    cat ~/.ssh/id_rsa.pub
    ```
    
    b. windows系统
    ```
    1. 安装git，从程序目录打开 "Git Bash" 
    2. 键入命令：ssh-keygen -t rsa -C "email@email.com" "email@email.com"是github账号
    3. 提醒你输入key的名称，你可以不用输入，直接3个回车，就OK了；
    4. 在C:\Documents and Settings\Administrator\下产生两个文件：id_rsa和id_rsa.pub
    5. 把4中生成的密钥文件复制到C:\Documents and Settings\Administrator\.ssh\ 目 录下。
    6. 用记事本打开id_rsa.pub文件，复制内容 
    ```
    c. mac  
    ```
    ssh-keygen -t rsa -C "ben@xxx.com"
    cat ~/.ssh/id_rsa.pub
    ```
2. 设置ssh公钥  
    a. 全局配置  
    ```
    成功登陆后：设置 ---> SSH密钥  
    这里配置的权限认证，拥有登陆用户的全部权限。  
    ```
    <img src="attachment/images/gitlab/添加ssh密钥（全局）.png" width = "800" heigth = "400" alt = "添加ssh密钥（全局）" align = center />
    b. 部署密钥  
    ```
    使用部署密钥只读访问项目  
    成功登陆后：项目 ---> 设置 ---> 版本库 ---> 部署密钥
    ```
    <img src="attachment/images/gitlab/部署密钥.png" width = "800" heigth = "400" alt = "部署密钥" align = center />  

### 项目权限控制
1. 项目可见性   
    > 控制项目的可见范围  

    <img src="attachment/images/gitlab/权限管理1.png" width = "800" heigth = "400" alt = "权限管理1" align = center />
    a. public:  
    > The project can be accessed without any authentication.
    
    1. Disabled
    2. Only team members
    3. Everyone with access  
    
    b. Internal
    > The project can be accessed by any logged in user.
    
    1. Disabled
    2. Only team members
    3. Everyone with access
     
    c. Private
    > Project access must be granted explicitly to each user.
    
    1. Disabled
    2. Only team members
    
2. 保护分支  
    <img src="attachment/images/gitlab/保护分支.png" width = "800" heigth = "400" alt = "保护分支" align = center />
    默认情况下，保护分支被设计为：  

    * 除了主程序员外，禁止其他所有人员创建分支
    * 除了主程序员外，禁止其他所有人员推送
    * 禁止任何人 强制推送此分支
    * 禁止任何人 删除此分支

3. 保护标签  
    <img src="attachment/images/gitlab/保护标签.png" width = "800" heigth = "400" alt = "保护标签" align = center />
    默认情况下，保护标签被设计为：

    *  除了主程序员外，禁止其他所有人员创建标签
    *  任何人 更新此标签
    *  任何人 删除此标签
