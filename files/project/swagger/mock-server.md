# swagger-mock-api
## 目前进度
101.200.194.158已经搭好环境,使用端口8500,启动命令
```
grunt connect
```
- 项目代码安装在/root/node_modules/swagger-mock-api
- 配置文件/root/Gruntfile.js
```
swaggerFile: path.join('http://101.200.194.158:8400/juzi-swagger/json/shequ/', 'v4.0.json'),
```
没有取到swagger中设置的默认值,资料有提到使用x-chance-type="fixed", c-chance-value=1这样就可以,但是swagger-php里写x-chance时报错,也许是写的地方不对,可以再尝试
## 参考
- [https://www.npmjs.com/package/swagger-mock-api](https://www.npmjs.com/package/swagger-mock-api)
- [grunt](http://www.jianshu.com/p/a339f2dc3823)
- [输出值chance](http://chancejs.com/#timestamp)
- [grunt](https://gruntjs.com/getting-started#preparing-a-new-grunt-project)