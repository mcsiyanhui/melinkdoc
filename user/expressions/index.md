---
layout: page
title: 用户动态表情接口
nav-index: 6
---
用户动态表情相关接口 - *表情me App专用

获取用户动态表情列表
----------------

地址:`/v1/{app_id}/user/expressions`

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
        "id":111,
        "name":"动态表情图片名称",
        "img_url":"动态表情图片地址",
        "is_default":"是否默认动态表情",
        "base_role_id":1,
        "sort":11,
        "update_time": "2014/12/02 17:01:44"
        "write_time": "2014/12/02 16:58:58"
   }, //...
]
{% endhighlight %}



获取用户表情详情
----------------

地址:`/v1/{app_id}/user/expression/{expressionid}`

方法:`GET`

说明:此接口将返回某一个表情的详细关联信息

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| logintoken     |String  |用户登录令牌识别码                    |*是 |

返回值:
{% highlight js %}
{
    "id":123,
    "name":"表情名称",
    "img_url":"表情图片地址",
    "is_default":true,
    "base_roleid":111 //此表情的来源角色ID
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


新增用户动态表情
----------------

地址:`/v1/{app_id}/user/expression/{expressionid}`

方法:`POST`

说明:expressionid 为0时，表示新增，img_data的key和value不参与签名

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| logintoken     |String  |用户登录令牌识别码                    |*是 |
| name           |String  |动态表情名称                          |*新增必传|
| img_data       |String  |拼接好的动态表情图片（base64字符串），不参与签名         |*新增必传|
| base_role_id    |Int     |此动态表情的来源角色ID                   |*新增必传, 无法修改|
| is_default     |int    |是否为默认动态表情,1是0不是                      |否|
| expression_material_ids   |JsonArray   |素材ID列表,[1,2,3,4]           |否 |
| adjustments    |JsonArray   |素材变换列表.['1','2','3']       |否 |


返回值:
{% highlight js %}
 {
 "id":11, //然后可以根据id来查询刚才更新的详细信息
 },

{% endhighlight %}

删除用户动态表情
----------------

地址:`/v1/{app_id}/user/expression/{expressionid}`

方法:`DELETE`

说明:动态表情生成过程比较容易,删除无需`name`参数确认

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| logintoken     |String  |用户登录令牌识别码                    |*是 |

返回值:
{% highlight js %}
{}
{% endhighlight %}
