me Link 文档
================
**版本** v0.4

App接入
----------------

* 参考[App接入指南](resources/app_link.md)

发起API请求
----------------

**API根路径** - `https://api.stampmeapp.com/{v1}/{appid}/`, 其中 `/{v1}` 为API版本号, `{appid}` 为应用ID  
({appid}的获取方式,参考 **App接入** 部分) 
测试API采用 `HTTP` 请求方式, 线上API只支持 `HTTPS`  

若需要请求所有的大头贴素材分组,则在根路径下加上大头贴素材资源的子路径:   https://api.stampmeapp.com/{v1}/{appid}/materials/expression/group.json  

如果是 `curl` 测试的话,完整的请求如下:  

```shell
curl -u appid:appsecret -H 'User-Agent: MyApp (yourname@example.com)' https://api.stampmeapp.com/{v1}/{appid}/materials/expression/groups.json
```
如果需要创建大头贴素材, 使用的是同一个资源，不同的是需要加上 `Content-Type` :  

```shell
curl -u appid:appsecret \
  -H 'Content-Type: Application/json' \
  -H 'User-Agent: MyApp (yourname@example.com)' \
  -d '{ "name": "配饰1" }' \
  https://api.stampmeapp.com/{v1}/{appid}/emoticons/groups.json
```

数据格式
-----------------

API仅支持`JSON`格式, 该`JSON`数据没有根元素, 其中的属性字段我们采用 `snake_case` 来描述  
当对API使用 `POST` 和 `PUT` 方法时, 请在请求头部加入 `Content-Type: Application/json; charset=utf-8`  
**所有的API请求以 .json 结尾,代表我们仅接受与返回JSON**  


使用HTTP缓存  
----------------
为提高接入应用的请求和响应速度,同时降低服务器负载,多数(尤其是数据量大)的返回数据我们会加上 `Last-Modified` 头部, 当第一次请求
某个资源时,保存该 `Last-Modified` 值, 后续的请求将该值作为 `If-Modified-Since` 重新发回服务器,如果资源没有任何变化, 服务器则
返回 `304 Not Modified`  

错误处理
---------------

当API服务器遇到问题时,你会看到 5xx 的错误反馈, 举例如下:  
* `500 API Server Down`
* `502 Bad Gateway`
* `503 Service Unavailable`
* `504 Gateway Timeout`

可用API列表
-----------------

* [Auth](resources/auth.md) - App认证授权相关接口
* [User Basic](resources/user_basic.md) - 用户基本接口
* [User Roles](resources/user_roles.md) - 用户角色相关接口
* [User Emoticons](resources/user_emoticons.md) - 用户大头贴相关接口
* [User Expressions](resources/user_expressions.md) - 用户动态表情相关接口
* [Materials](resources/materials.md) - 分组与素材相关接口(Me App专用)
* [Open](resources/open.md) - 对外开放数据接口
* [Page](resources/page.md) - 页面接入接口

