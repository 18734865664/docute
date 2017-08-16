# swagger注释说明

<span id="参考文档"></span>
> 参考文档
[https://github.com/OAI/OpenAPI-Specification/blob/master/versions/2.0.md#infoObject](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/2.0.md#infoObject)

## 1. 安装swagger
```
composer global require zircote/swagger-php
```
global参数可以多个项目使用同一个swagger-php,并且不会在项目代码里引入swagger-php代码

## 2. 运行代码
写完项目代码注释后运行:
```
~/.composer/vendor/bin/swagger /data/ngx_openresty/nginx/html/forum-juzi/application --bootstrap /data/ngx_openresty/nginx/html/forum-juzi/application/swagger/constants.php -o /data/ngx_openresty/nginx/html/swagger/juzi-swagger/json/shequ/v4.0.json
```
- 参数1为需要扫描的[项目文件夹](#扫描文件夹)
- bootstrap参数值为当前的[常量文件](#定义常量)
- o参数值为最终生成json文件的目录,在juzi-swagger项目的json文件夹下,需要创建自己项目的文件夹,按版本命名


## 3. hello world

<span id="扫描文件夹"></span>
### 新建项目目录
在项目的controller同级文件夹里新建swagger文件夹,swagger单独定义的文件全放入
```
cd 项目contoller同级文件夹
mkdir swagger
```
> 运行时会扫描指定文件夹的所有文件,注释是写到controller里的,所以最好能同级放

<span id="定义常量"></span>
### 定义常量
```
<?php
vim swagger/constants.php
define("API_HOST", (ini_get('yaf.environ') === "production") ? "api.app.happyjuzi.com" : "testapi.app.happyjuzi.com");
define("VERSION", '4.0');
```

### 数据类型(array\string\integer)
- array —— item
```
/*
 *
 *  @SWG\Property(
 *          property="list",
 *          type="array",
 *          @SWG\Items(ref="#/definitions/emoticon")
 *  )
 *
 * @SWG\Definition(
 *     definition="emoticon",
 *     @SWG\Property(
 *          property="id",
 *          type="integer",
 *          format="int32"
 *      ),
 *     @SWG\Property(
 *        property="url",
 *        type="string"
 *     ),
 *     @SWG\Property(
 *          property="thumb",
 *          type="string"
 *      ),
 *     @SWG\Property(
 *          property="thumb_jpg",
 *          type="string"
 *     ),
 *     @SWG\Property(
 *          property="width",
 *          type="integer",
 *          format="int32"
 *     ),
 *     @SWG\Property(
 *          property="height",
 *          type="integer",
 *         format="int32"
 *     ),
 *     @SWG\Property(
 *          property="html",
 *          type="string"
 *      )
 * )
 */
```
- string
```
/*
 *     @SWG\Property(
 *          property="thumb_jpg",
 *          type="string"
 *     )
 */
```
- integer —— format: int32/int64
```
/*
 *     @SWG\Property(
 *          property="height",
 *          type="integer",
 *         format="int32"
 *     ),
 */
```
- object
```
/*
 * @SWG\Property(property="data", type="object", ref="#/definitions/emoticon-list")
 */
```

### 基本信息
```
vim swagger/info.php
/**
 * @SWG\Swagger(
 *     schemes={"http"},
 *     host=API_HOST,
 *     basePath="/shequ",
 *     version=VERSION,
 *     consumes={"application/x-www-form-urlencoded"},
 *     produces={"application/json"},
 *     @SWG\Info(
 *         title="社区api",
 *         description="这是社区的api",
 *         termsOfService="http://api.app.happyjuzi.com",
 *         @SWG\Contact(
 *             email="api@happyjuzi.com"
 *         ),
 *     ),
 *     @SWG\ExternalDocumentation(
 *         description="Swagger ui",
 *         url="http://101.200.194.158:8400/swagger-ui/dist/shequ.html"
 *     )
 * )
 */
```
- basePath —— host里统一添加的路径
- comsumes —— 输入使用的格式,可多个,用‘,’隔开
- produces —— 输出使用的格式,可多个,用‘,’隔开

> 其它参照[参考文档](#参考文档)

### 抽取公共部分
抽取出输入输出共同的部分,单独定义为definition
. 公共输入
```
/**
 * @SWG\Definition(
 *      definition="base-input",
 *      required={"ver", "uid"},
 *      @SWG\Property(
 *         property="ver",
 *         type="string",
 *         default=VERSION,
 *         example=VERSION
 *      ),
 *      @SWG\Property(
 *         property="uid",
 *         type="integer",
 *         format="int64",
 *         default="4087386321629213",
 *         example="4087386321629213"
 *      ),
 *      @SWG\Property(
 *         property="accesstoken",
 *         type="string",
 *         default="a067c7405bffaf2bffea5a5d999f82f0",
 *         example="a067c7405bffaf2bffea5a5d999f82f0"
 *      )
 * )
 */
```
使用示例
```
/*
 * @SWG\Definition(
 *      definition="emoticon-create-input",
 *      allOf={
 *          @SWG\Schema(ref="#/definitions/base-input"),
 *          @SWG\Schema(
 *              required={"img"},
 *              @SWG\Property(
 *                  property="img",
 *                  type="string",
 *                  default="http://images11.app.happyjuzi.com/content/201708/09/598a92fda694e.gif",
 *                  example="http://images11.app.happyjuzi.com/content/201708/09/598a92fda694e.gif"
 *              )
 *         )
 *     }
 * )
 */
```
. 公共输出
```
/**
 * @SWG\Definition(
 *         definition="base-response",
 *         required={"code", "msg"},
 *         @SWG\Property(
 *             property="code",
 *             type="integer",
 *             format="int32"
 *         ),
 *         @SWG\Property(
 *             property="msg",
 *             type="string"
 *         )
 * )
 */
```
使用示例

```
/*
 * @SWG\Response(
 *   response="error",
 *   description="缺少参数",
 *   @SWG\Schema(ref="#/definitions/base-response")
 * )
 */
```

### 项目代码中的注释
#### post请求
```
   /**
     * @SWG\Post(
     *   path="/emoticon/create",
     *   summary="add emoticon",
     *   tags={"postings"},
     *   description="添加表情,第一次添加正常返回,第二次添加返回已操作",
     *   operationId="addEmoticon",
     *   @SWG\Parameter(
     *         name="body",
     *         in="body",
     *         description="添加表情",
     *         required=true,
     *         @SWG\Schema(ref="#/definitions/emoticon-create-input"),
     *   ),
     *   @SWG\Response(response="default", ref="#/responses/create-emoticon"),
     *   @SWG\Response(response="200", ref="#/responses/error")
     * )
     */
```
- path —— 访问路径
- summary —— 总结
- tags —— 标签,会在预览页面相应标签里出现,可添加多个,以‘,’隔开
- description —— 简介
- operationId —— 文档里唯一标识此操作
- @SWG\Parameter —— 输入的参数,@SWG\Schema后面[详细介绍](#@SWG\Schema)
- parameter里in有值
1. body —— post中body里id=12
2. query —— index.php?id=12
3. path —— url里直接/id/12

#### get请求
```
/**
     * @SWG\Get(
     *   path="/emoticon/emtlist",
     *   summary="list of emoticon",
     *   tags={"postings"},
     *   description="表情包列表.ts与最后一次返回ts不同时返回所有的表情包;如果与最后一次ts相同则返回20010,表示不需要更新app端",
     *   operationId="emtlist",
     *   @SWG\Parameter(
     *        name="body",
     *        in="query",
     *        ref="#/definitions/emoticon-list-input"
     *   ),
     *   @SWG\Response(response="default", ref="#/responses/emoticon-list"),
     *   @SWG\Response(response="200", ref="#/responses/error")
     * )
     */
```

### 基本概念
- definition
- parameter
- property
- response
- item

### 基本写法

<span id="@SWG\Schema"></span>
#### @SWG\Schema
. post里参数
```
@SWG\Schema(ref="#/definitions/emoticon-create-input")
```
其中ref里引用definitions中的emoticon-create-input,
```
 /**
 * @SWG\Definition(
 *      definition="emoticon-create-input",
 *      allOf={
 *          @SWG\Schema(ref="#/definitions/base-input"),
 *          @SWG\Schema(
 *              required={"img"},
 *              @SWG\Property(
 *                  property="img",
 *                  type="string",
 *                  default="http://images11.app.happyjuzi.com/content/201708/09/598a92fda694e.gif",
 *                  example="http://images11.app.happyjuzi.com/content/201708/09/598a92fda694e.gif"
 *              )
 *         )
 *     }
 * )
 */
```
- definition 表示名字
- allOf表示由下面几个一起组成


- @SWG\Schame
- @SWG\Response
- @SWG\Get
- @SWG\Post


所有参数都以ref形式在php真实代码中出现

## get方法参数设置

## post方法参数设置

将公共部分弄成base-reaponse的definition

## 返回值参数设置

##

