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

在项目根目录下创建sonar-project.properties文件
```
# must be unique in a given SonarQube instance
sonar.projectKey=my:project
# this is the name and version displayed in the SonarQube UI. Was mandatory prior to SonarQube 6.1.
sonar.projectName=My project
sonar.projectVersion=1.0
 
# Path is relative to the sonar-project.properties file. Replace "\" by "/" on Windows.
# This property is optional if sonar.modules is set. 
sonar.sources=.
#sonar.inclusions=./path1,./path2
#sonar.exclusions=./somepath
 
# Encoding of the source code. Default is default system encoding
#sonar.sourceEncoding=UTF-8
```
在项目根目录下运行以下命令进行分析
```
sonar-scanner
```