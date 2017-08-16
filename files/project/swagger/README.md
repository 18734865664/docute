# swagger
## 预览
### 地址
. 社区预览地址:
[http://101.200.194.158:8400/swagger-ui/dist/shequ.html](http://101.200.194.158:8400/swagger-ui/dist/shequ.html)

. 社区json地址:
[http://101.200.194.158:8400/juzi-swagger/json/shequ/v4.0.json](http://101.200.194.158:8400/juzi-swagger/json/shequ/v4.0.json)

也可以将生成的json地址输入
<img src="attachment/images/swagger_1.png" alt="登陆页面" align=center />
> 点击“explore”后将生成预览

### 相关项目GIT
. 放置json文件
```
git clone ssh://自己名字全拼@111.203.201.131:8022/var/www/juzi-swagger.git
```
. UI预览
```
git clone ssh://自己名字全拼@111.203.201.131:8022/var/www/swagger-ui.git
cp /data/ngx_openresty/nginx/html/swagger/swagger-ui/dist/index.html /data/ngx_openresty/nginx/html/swagger/swagger-ui/dist/shequ.html
vim /data/ngx_openresty/nginx/html/swagger/swagger-ui/dist/shequ.html
```
将shequ.html中的
```
const ui = SwaggerUIBundle({
    url: "http://petstore.swagger.io/v2/swagger.json",
```
url修改成项目对应的json地址
```
const ui = SwaggerUIBundle({
    url: "http://101.200.194.158:8400/juzi-swagger/json/shequ/v4.0.json",
```
## [注释书写](http://192.168.10.70:8033/#/project/swagger/backend-write)
