---
layout: page
title: 概述
nav-index: 0
---
App接入
----------------

* 参考[App接入指南](/app/link/)

发起API请求
----------------

**API根路径** - `https://api.stampmeapp.com/{v1}/{app_id}`, 其中 `/{v1}` 为API版本号, `{app_id}` 为设备的app_id
({app_id}的获取方式,参考 **App接入** 部分) 
测试API采用 `HTTP` 请求方式, 线上API只支持 `HTTPS`  

若需要请求所有的大头贴素材分组,则在根路径下加上大头贴素材资源的子路径:   https://api.stampmeapp.com/{v1}/{app_id}/materials/emoticons

具体请参考 [App接入指南](/app/link/)


数据格式
-----------------

API仅支持`JSON`格式, 该`JSON`数据没有根元素, 其中的属性字段我们采用 `snake_case` 来描述  
当对API使用 `POST` 和 `PUT` 方法时, 请在请求头部加入 `Content-Type: Application/json; charset=utf-8`  


错误处理
---------------

当API服务器遇到问题时,你会看到 5xx 的错误反馈, 举例如下:  

* `500 API Server Down`  
* `502 Bad Gateway`  
* `503 Service Unavailable`  
* `504 Gateway Timeout`  

可用API列表
-----------------

* [Auth](/app/auth/) - App认证授权相关接口
* [User Basic](/user/basic/) - 用户基本接口
* [User Roles](/user/roles/) - 用户角色相关接口
* [User Emoticons](/user/emoticons/) - 用户大头贴相关接口
* [User Expressions](/user/expressions/) - 用户动态表情相关接口
* [Materials](/materials/) - 分组与素材相关接口(Me App专用)
* [Open](/open/) - 对外开放数据接口
* [Page](/page/) - 页面接入接口
* [Share](/share/) - 分享接口

