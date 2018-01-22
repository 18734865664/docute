# 测试环境自助部署
## 背景
&emsp;&emsp;为规范测试环境的使用，将测试服务器root权限回收，测试环境分为多套环境并行：   
1. 普通账号家目录下可以单独部署一套测试环境。
    1.  目前只开放测试人员私有账号创建私有测试环境；
    2.  测试环境由运维维护；
    3.  端口分配由运维管理；
    4.  访问使用IP+端口的形式
2.  data 目录下有一套公用的测试环境
    1. 公用测试环境代码由CI流程自动部署；
    2. 访问采用域名形式；  
    
&emsp;&emsp;为方便私有测试环境的代码部署，搭建了本套系统，系统由运维进行维护。
## 系统基本情况
### 访问方式
&emsp;&emsp;http://192.168.10.150:8090/
### 开通部署功能的账号
    
    每个账号有新的部署需求，联系运维对端口进行规划

<table> 
    <tr>
        <td>账号</td>
        <td>项目</td>
        <td>nginx端口</td>
        <td>后端服务端口</td>
    </tr>
    <tr>
        <td>zhangxinxin</td>
        <td>api-juzi</td>
        <td>10701</td>
        <td>10702</td>
    </tr>
    <tr>
         <td rowspan='5'>fankaiqiang</td>
         <td>admin-juzi</td>
         <td>11001</td>
         <td></td>
    </tr>
    <tr>
        <td>api-juzi</td>
        <td>11002</td>
        <td>11003</td>
    </tr>
    <tr>
        <td>pc-juzi</td>
        <td>11004</td>
        <td></td>
    </tr>
    <tr>
        <td>juzi-m</td>
        <td>11005</td>
        <td>11006</td>
    </tr>
    <tr>
        <td>forum-juzi</td>
        <td>11007</td>
        <td></td>
    </tr>
    <tr>
         <td rowspan='5'>yangminli</td>
         <td>admin-juzi</td>
         <td>10400</td>
         <td></td>
    </tr>
    <tr>
        <td>api-juzi</td>
        <td>10401</td>
        <td>10402</td>
    </tr>
    <tr>
        <td>pc-juzi</td>
        <td>10403</td>
        <td></td>
    </tr>
    <tr>
        <td>juzi-m</td>
        <td>10404</td>
        <td>10405</td>
    </tr>
    <tr>
        <td>forum-juzi</td>
        <td>10406</td>
        <td></td>
    </tr>
    <tr>
         <td rowspan='5'>liuyang</td>
         <td>admin-juzi</td>
         <td>10200</td>
         <td></td>
    </tr>
    <tr>
        <td>api-juzi</td>
        <td>10201</td>
        <td>10202</td>
    </tr>
    <tr>
        <td>pc-juzi</td>
        <td>10203</td>
        <td></td>
    </tr>
    <tr>
        <td>juzi-m</td>
        <td>10204</td>
        <td>10205</td>
    </tr>
    <tr>
        <td>forum-juzi</td>
        <td>10206</td>
        <td></td>
    </tr>
    <tr>
         <td rowspan='6'>wangliping</td>
         <td>admin-juzi</td>
         <td>10100</td>
         <td></td>
    </tr>
    <tr>
        <td>api-juzi</td>
        <td>10110</td>
        <td>10108</td>
    </tr>
    <tr>
        <td>pc-juzi</td>
        <td>10103</td>
        <td></td>
    </tr>
    <tr>
        <td>juzi-m</td>
        <td>10102</td>
        <td>10101</td>
    </tr>
    <tr>
        <td>forum-juzi</td>
        <td>10105</td>
        <td></td>
    </tr>
    <tr>
        <td>static-frame</td>
        <td>10109</td>
        <td></td>
    </tr>
</table>

## 使用流程
1. 账号注册

    登陆账号可以自行注册，也可以联系运维开通
    处于未登录状态，可以查看构建历史/输出，但不能触发新的构建

<img src="attachment/images/publish_test_env/登陆.png" width = "700" height = "300" alt="登陆页面" align=center />
<img src="attachment/images/publish_test_env/账号密码.png" width = "700" height = "300" alt="账号密码" align=center />

2.选择要部署的项目

    登陆后，在首页选择要部署的项目

<img src="attachment/images/publish_test_env/选择项目.png" width = "700" height = "300" alt="选择项目" align=center />

3.开始构建

    选择项目后，可以开始新的构建操作

<img src="attachment/images/publish_test_env/开始构建.png" width = "700" height = "300" alt="开始构建" align=center />
    
    选择要部署的分支

<img src="attachment/images/publish_test_env/开始构建2.png" width = "700" height = "300" alt="开始构建2" align=center />

4.构建过程

    选定触发构建后，可以在历史栏看到有构建正在执行

<img src="attachment/images/publish_test_env/正在部署.png" width = "700" height = "300" alt="正在部署" align=center />

    有本次构建分支的一些基本情况

<img src="attachment/images/publish_test_env/详情.png" width = "700" height = "300" alt="详情" align=center />

    构建过程中可以实时的查看相应的输出

<img src="attachment/images/publish_test_env/过程输出.png" width = "700" height = "300" alt="过程输出" align=center />

