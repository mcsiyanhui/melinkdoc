---
layout: page
title: 用户大头贴接口
nav-index: 5
---
用户大头贴相关接口 - *表情me App专用

获取用户大头贴列表
----------------

地址:`/v1/{app_id}/user/emoticons`

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
        "id":123, //大头贴ID
        "img_url":"大头贴图片地址",
        "is_default":true,
        "base_role_id":"基于角色id",
        "gender":"0女1男",
        "name":"大头贴名称",
        "sort":2, //排序
        "update_time":"2014-11-28 17:01:47"//更新时间
        "write_time":"2014-11-28 17:01:47"//创建时间
    }, //...

]
{% endhighlight %}

获取用户大头贴详情
----------------

地址:`/v1/{app_id}/user/emoticon/{emoticonid}`

方法:`GET`

说明:此接口将返回某一个大头贴的详细关联信息

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| logintoken     |String  |用户登录令牌识别码                    |*是 | 

返回值:
{% highlight js %}
{
    "id":123,
    "name":"大头贴名称",
    "gender":0, //0表示女性, 1表示男性
    "img_url":"大头贴图片地址",
    "is_default":true,
    "base_roleid":111 //此大头贴的来源角色ID
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


新增或更新用户大头贴
----------------

地址:`/v1/{app_id}/user/emoticon/{emoticonid}`

方法:`POST`

说明:当传递`emoticonid`为0时，表示添加此用户的大头贴信息，另外多个`materialid`根据以下方式传递,

注意:adjustments数组长度必须和material_ids相同，如果没有形变，请留空，img_data的key和value不参与签名

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| logintoken     |String  |用户登录令牌识别码                    |*是 |
| name           |String  |大头贴名称                          |*新增必传|
| gender         |Int     |大头贴性别                          |*新增必传|
| img_data       |String  |拼接好的大头贴图片（base64字符串），不参与签名         |*新增必传|
| base_role_id    |Int     |此大头贴的来源角色ID                   |*新增必传, 无法修改，如果重新创建的，传入0|
| is_default     |Int    |是否为默认大头贴,是传入1，否传入0                      |否|
| material_ids   |JsonArray   |素材ID列表,[1,2,3,4]           |否 |
| adjustments    |JsonArray   |素材变换列表.['1','2','3']       |否 |

返回值:
{% highlight js %}
{
    "Id":11, //然后可以根据Id来查询刚才更新的详细信息
}
{% endhighlight %}

删除用户大头贴
----------------

地址:`/v1/{app_id}/user/emoticon/{emoticonid}`

方法:`DELETE`

说明:emoticonid,Int,大头贴ID

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| logintoken     |String  |用户登录令牌识别码                    |*是 |
| name           |String  |大头贴名称                         |*是 |

返回值:
{% highlight js %}
{}
{% endhighlight %}

(暂时不需要，设置默认通过更新用户大头贴接口)设置用户默认大头贴
----------------

地址:`/user/emoticon/{emoticonid}/default`

方法:`POST`

说明:设置该用户默认大头贴,emoticonid,Int,大头贴ID

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| logintoken     |String  |用户登录令牌识别码                    |*是 |


返回值:
{% highlight js %}
{}
{% endhighlight %}
