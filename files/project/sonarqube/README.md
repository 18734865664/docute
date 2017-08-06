介绍

sonarqube

sonarqube是一个用于代码质量管理的开源平台，用于管理源代码的质量，可以从多个维度检测代码质量
通过插件形式，可以支持包括php,java,C#,C/C++,PL/SQL,Cobol,JavaScrip,Groovy等等二十几种编程语言的代码质量管理与检测

sonar-scanner

sonar-scanner是sonarqube提供，配合sonarqube管理平台完成静态代码扫描的命令行工具，
其作用是根据配置规则(sonarqube管理平台设置)对代码进行扫描，然后将扫描结果提交到服务端(sonarqube管理平台)进行分析，
最后在sonarqube管理平台以各维度展示分析结果。

由于sonarqube管理平台（[http://192.168.10.153:9000](https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner)）已在服务器上搭建共用，本文不介绍其安装。
下文主要介绍客户端工具sonar-scanner的安装、使用以及管理平台查看相关分析结果等内容。

安装

1、下载压缩包[sonar-scanner](https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner)，下载完成后解压到本地目录，例如/usr/local/sonar-scanner

2、修改安装目录/conf/sonar-scanner.properties文件sonar.host.url值为SonarQube服务器地址，例如
```
# Default SonarQube server
sonar.host.url=http://192.168.10.153:9000
```
3、配置环境变量
```
export PATH=$PATH:本地安装目录/bin/
```

4、检验安装是否正确。sonar-scanner -h

使用

1、在项目根目录下创建sonar-project.properties文件，复制以下内容到文件中，
注意要根据属性含义结合项目实际进行修改，sonar.projectKey为唯一标识属性，
必须设置
```
# must be unique in a given SonarQube instance
sonar.projectKey=api
# this is the name and version displayed in the SonarQube UI. Was mandatory prior to SonarQube 6.1.
sonar.projectName=api
sonar.projectVersion=3.8
 
# Path is relative to the sonar-project.properties file. Replace "\" by "/" on Windows.
# This property is optional if sonar.modules is set. 
sonar.sources=.
#sonar.inclusions=./path1,./path2
#sonar.exclusions=./somepath
 
# Encoding of the source code. Default is default system encoding
#sonar.sourceEncoding=UTF-8
```
2、在项目根目录下运行以下命令进行分析
```
sonar-scanner
```

3、访问sonarqube管理平台（[http://192.168.10.153:9000](https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner)）查看分析结果

<img src="attachment/images/sonarqube01.png" width = "700" height = "300" align=center />

<img src="attachment/images/sonarqube02.png" width = "700" height = "300" align=center />

<img src="attachment/images/sonarqube03.png" width = "700" height = "300" align=center />

<img src="attachment/images/sonarqube04.png" width = "700" height = "300" align=center />

<img src="attachment/images/sonarqube05.png" width = "700" height = "300" align=center />

<img src="attachment/images/sonarqube06.png" width = "700" height = "300" align=center />

<img src="attachment/images/sonarqube07.png" width = "700" height = "300" align=center />

<img src="attachment/images/sonarqube08.png" width = "700" height = "300" align=center />

<img src="attachment/images/sonarqube09.png" width = "700" height = "300" align=center />

<img src="attachment/images/sonarqube10.png" width = "700" height = "300" align=center />

<img src="attachment/images/sonarqube11.png" width = "700" height = "300" align=center />

<img src="attachment/images/sonarqube12.png" width = "700" height = "300" align=center />

<img src="attachment/images/sonarqube13.png" width = "700" height = "300" align=center />