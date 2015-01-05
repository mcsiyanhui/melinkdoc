---
layout: page
title: 用户角色接口
nav-index: 4
---
用户角色相关接口 - *表情me App专用

获取用户角色
----------------

地址:`/v1/{app_id}/user/roles`

方法:`GET`

说明:无

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| logintoken     |String  |用户登录令牌识别码                    |*是 | 

返回值:
{% highlight js %}
[
    {
        "id":123, //角色ID
        "img_url":"角色图片地址",
        "is_default":true,
        "base_role_id":"基于角色id",
        "gender":"0女1男",
        "name":"角色名称",
        "sort":2, //排序
        "update_time":"2014-11-28 17:01:47"//更新时间
        "write_time":"2014-11-28 17:01:47"//创建时间
    }, //...

]
{% endhighlight %}

获取用户角色详情
----------------

地址:`/v1/{app_id}/user/role/{roleid}`

方法:`GET`

说明:此接口请配合获取分组材料接口使用，这里将不返回用户所有素材内容，而仅是素材标识和分组标识

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| logintoken     |String  |用户登录令牌识别码                    |*是 |

返回值:
{% highlight js %}
{
    "id":123,
    "name":"角色名称",
    "gender":0, //0表示女性, 1表示男性
    "img_url":"角色图片地址",
    "is_default":true,
    "base_roleid":111 //此角色的来源角色ID
    "sort":2, //排序
    "update_time":"2014-11-28 17:01:47"//更新时间
    "write_time":"2014-11-28 17:01:47"//创建时间
    "materials":{
       {
            "id":111,
            "ename":"唯一标识", // 这里后台可以录入客户端原来对于某一个素材唯一标识, 免去重复编码
            "adjustment":{"zoom":100} //变形, 偏移, 缩放等
       }, //...
    }
}
{% endhighlight %}

新增或更新用户角色
----------------

地址:`/v1/{app_id}/user/role/{roleid}`

方法:`POST`

说明:当传递`roleid`为0时，表示更新此角色信息，另外多个`materialid`根据以下方式传递,

注意:adjustments数组长度必须和material_ids相同，如果没有形变，请留空

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| logintoken     |String  |用户登录令牌识别码                    |*是 |
| name           |String  |角色名称                          |*新增必传|
| gender         |Int     |角色性别                          |*新增必传|
| img_data       |String  |拼接好的角色图片（base64字符串）         |*新增必传|
| base_role_id    |Int     |此角色的来源角色ID                   |*新增必传, 无法修改，如果重新创建的，传入0|
| is_default     |Int    |是否为默认角色,是传入1，否传入0                      |否|
| material_ids   |JsonArray   |素材ID列表,[1,2,3,4]           |新增必传 |
| adjustments    |JsonArray   |素材变换列表.['1','2','3']       |新增必传 |

返回值:
{% highlight js %}
{
"id":11 //然后可以根据id来查询刚才更新的详细信息
}
{% endhighlight %}

删除用户角色
----------------

地址:`/v1/{app_id}/user/role/{roleid}`

方法:`DELETE`

说明:无

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| logintoken     |String  |用户登录令牌识别码                    |*是 |
| name           |String  |角色名                              |*是| 

返回值:
{% highlight js %}
{}
{% endhighlight %}
