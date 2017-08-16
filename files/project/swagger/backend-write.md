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

## 基本概念

### meta
- @SWG\Swagger 最外层meta,一定要有
- @SWG\Info 基本信息,一定要有
- @SWG\Tag 标签
- @SWG\ExternalDocumentation 定义外部文档url
- @SWG\Definition 定义对象,使用ref="#/definitions/名字"
- @SWG\Parameter 参数
- @SWG\Property Definition的属性
- @SWG\Response 返回值
- @SWG\Items 数组里的item
- @SWG\Schame 引用其它值
- @SWG\Get get请求
- @SWG\Post post请求

### 数据类型(array\string\integer\object)
<img src="attachment/images/swagger-data-type.png" alt="数据类型" align=center/>
- array —— item

```
/*
 *  @SWG\Property(
 *      property="list",
 *      type="array",
 *      @SWG\Items(ref="#/definitions/emoticon")
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

### 标签
可定义也可不定义,定义后按定义先后顺序显示,未定义按分析json文件的工具规则顺序排序

```
/*
 * @SWG\Tag(
 *   name="postings",
 *   description="关于帖子的操作",
 *   @SWG\ExternalDocumentation(
 *     description="更多关于帖子操作,@SWG\ExternalDocumentation用于定义额外的链接,可不写",
 *     url="http://swagger.io"
 *   )
 * )
 */
```
<p class="warning">可用于定义版本,但是标签之间没有承继关系,版本下就不能按照帖子评论等进行归类,版本下标签不能直接看到全部的api,需要往下版本查看继承的方法</p>


## 3. hello world

<span id="扫描文件夹"></span>
### 新建项目目录
在项目的controller同级文件夹里新建swagger文件夹,swagger单独定义的文件全放入
```
cd 项目contoller同级文件夹
mkdir swagger
```
> 运行时会扫描指定文件夹的所有文件,注释是写到controller里的,所以最好能同级放
> 最好是response/definition/parameter-in-query/parameter-in-body等文件分开,易于管理

<span id="定义常量"></span>
### 定义常量
```
<?php
vim swagger/constants.php
define("API_HOST", (ini_get('yaf.environ') === "production") ? "api.app.happyjuzi.com" : "testapi.app.happyjuzi.com");
define("VERSION", '4.0');
```

### 基本信息
一定要有一个info
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
 *                  type="string"
 *              )
 *         )
 *     }
 * )
 */
```
> emoticon-create-input使用参见[post请求](#post请求)

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

1. 最简单的使用,返回参数与base-response一样
```
/*
 * @SWG\Response(
 *   response="error",
 *   description="缺少参数",
 *   @SWG\Schema(ref="#/definitions/base-response")
 * )
 */
 ```

2. 返回参数还包含其它值
#### 最终结果
```
{
    "msg": "操作成功",
    "data": {
        "ts": 1499332851,
        "info": {
            "id": 15,
            "url": "http://images11.app.happyjuzi.com/content/201608/02/57a083805548c.gif!ac1.gif.webp",
            "thumb": "http://images11.app.happyjuzi.com/content/201608/02/57a083805548c.gif!th.gif",
            "thumb_jpg": "http://images11.app.happyjuzi.com/content/201608/02/57a083805548c.gif!th.jpg",
            "width": 360,
            "height": 270,
            "html": "<p><img class=\"load-img dom-img\" data-original=\"http://images11.app.happyjuzi.com/content/201608/02/57a083805548c.gif!ac1.gif.webp\" width=\"360\" height=\"270\" src=\"http://cdn.happyjuzi.com/static-frame/public/img/kong.png\"/></p>"
        }
    },
    "code": 1
}
```
#### swagger代码
 ```
 /*
 * @SWG\Response(
 *    response="create-emoticon",
 *    description="添加表情包返回值",
 *    @SWG\Schema(ref="#/definitions/emoticon-create-definition")
 * )
 *  1) 定义包含base-response与一个data字段,data又是引用了emoticon-data
 * @SWG\Definition(
 *     definition="emoticon-create-definition",
 *     allOf={
 *          @SWG\Schema(ref="#/definitions/base-response"),
 *          @SWG\Schema(
 *              required={"data"},
 *              @SWG\Property(property="data", type="object", ref="#/definitions/emoticon-data")
 *         )
 *     }
 * )
 *  2) emoticon=data的定义,这个结构又包含了emoticon的定义
 * @SWG\Definition(
  *     definition="emoticon-data",
  *     @SWG\Property(
  *          property="ts",
  *          type="integer",
  *          format="int32"
  *      ),
  *     @SWG\Property(
  *          property="info",
  *          type="object",
  *          ref="#/definitions/emoticon"
  *      )
  * )
  *  3) 最终emoticon的定义
  * <span id="emoticon的定义"></span>
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

### 项目代码中的注释
<span id="post请求"></span>
#### post请求
在项目代码中添加注释
```
   /**
     * @SWG\Post(
     *   path="/emoticon/create",
     *   summary="添加表情包",
     *   tags={"v4.0", "postings"},
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
- @SWG\Parameter里in有值
1. body —— post中body里id=12
2. query —— index.php?id=12
3. path —— url里直接/id/12
- @SWG\Response
1. response值:default或者其它状态码
2. ref为引用定义好的response

<span id="get请求"></span>
#### get请求
在项目代码中添加注释
```
/**
     * @SWG\Get(
     *   path="/emoticon/emtlist",
     *   summary="表情包列表",
     *   tags={"postings"},
     *   description="表情包列表.ts与最后一次返回ts不同时返回所有的表情包;如果与最后一次ts相同则返回20010,表示不需要更新app端",
     *   operationId="emtlist",
     *   @SWG\Parameter(
     *        name="query",
     *        in="query",
     *        ref="#/definitions/emoticon-list-input"
     *   ),
     *   @SWG\Response(response="default", ref="#/responses/emoticon-list"),
     *   @SWG\Response(response="200", ref="#/responses/error")
     * )
     */
```
input
```
/**
 * @SWG\Definition(
 *      definition="emoticon-list-input",
 *      allOf={
 *          @SWG\Schema(ref="#/definitions/base-input"),
 *          @SWG\Schema(
 *              @SWG\Property(
 *                  property="ts",
 *                  type="integer",
 *              )
 *         )
 *     }
 * )
 */
```
response
```
/*
 * @SWG\Response(
 *    response="emoticon-list",
 *    description="表情包列表",
 *    @SWG\Schema(ref="#/definitions/emoticon-list-definition")
 * )
 *
 * @SWG\Definition(
 *     definition="emoticon-list-definition",
 *     allOf={
 *          @SWG\Schema(ref="#/definitions/base-response"),
 *          @SWG\Schema(
 *              required={"data"},
 *              @SWG\Property(property="data", type="object", ref="#/definitions/emoticon-list")
 *         )
 *     }
 * )
 */
 ```
 ```
/*
 * @SWG\Definition(
 *     definition="emoticon-list",
 *     @SWG\Property(
 *          property="ts",
 *          type="integer",
 *          format="int32"
 *      ),
 *     @SWG\Property(
 *          property="total",
 *          type="integer",
 *          format="int32"
 *     ),
 *     @SWG\Property(
 *          property="list",
 *          type="array",
 *          @SWG\Items(ref="#/definitions/emoticon")
 *      )
 * )
 */
```
> emoticon定义见[emoticon的定义](#emoticon的定义)
