---
layout: page
title: 素材接口
nav-index: 7
---

分组与素材相关接口 - *表情me App专用

获取角色,大头贴素材分组与素材
----------------

地址:`/v1/{app_id}/materials/roles`
地址:`/v1/{app_id}/materials/emoticons`

方法:`GET`

说明:此接口没有缓存,用来初始化第一次安装

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| group_only    |int |如果为`1`,则只返回分组信息,如果为`0`则返回全部，默认为`0`   |否 |

返回值:
{% highlight js %}
{
        "male": [
            {
                "auto_version": 1.0, //此分组版本号
                "custom_key_value": "{}", //自定义kv字段，json格式字符串
                "custom_tags": "[]", //自定义tag字段，json格式字符串
                "ename": "此分组英文短名",
                "gender": 1, //1表示男性
                "locale_ename": "chn",//分组的主要所属国际化
                "locales":["chn"],        //一个分组所属多个国家预留
                "groups": [
                    {
                        "auto_version": 1.0, //此分组版本号
                        "custom_key_value": "{}", //自定义kv字段，json格式字符串
                        "custom_tags": "[]", //自定义tag字段，json格式字符串
                        "ename": "此分组英文短名",
                        "gender": 1, //1表示男性
                        "groups": [...],//支持嵌套，可能有N级
                        "materials":[...],//省略此分组下的素材
                        "icon_url": "分组图标地址",
                        "id": 1,
                        "intro": "分组简介",
                        "name": "分组名称",
                        "parent_group_id": 0,//父分组id
                        "sort": 1, //排序
                        "type": 1  //1表示角色使用，2表示大头贴使用，3表示通用
                        "locale_ename": "chn", //分组的主要所属国际化
                        "locales":["chn"],        //一个分组所属多个国家预留

                    }, //...省略多个子分组
                ],
                "materials": [
                        {
                            "custom_key_value": "11",
                            "custom_tags": "11",
                            "ename": "aa1",
                            "id": 1,
                            "img_url_1":"动态表情素材图片地址，nie.1图片",
                            "img_url_2":"动态表情素材图片地址，nie.2图片",
                            "img_url_3":"动态表情素材图片地址，nie.3图片",
                            "img_url_4":"动态表情素材图片地址，nie.4图片",
                            "img_url_5":"动态表情素材图片地址，缩略图用",
                            "is_animation": true,
                            "name": "aa",
                            "sort": 1,
                            "locales":["chn", "jpn"],        //一个素材所属多个国家
                        }, ...//省略此分组下的多个素材
                ],
                "icon_url": "分组图标地址",
                "id": 1,
                "intro": "分组简介",
                "name": "分组名称",
                "parent_group_id": 0,//父分组id
                "sort": 1, //排序
                "test": false, //此素材分组是否为测试用
                "type": 1  //1表示角色使用，2表示大头贴使用，3表示通用

            },//...省略顶级分组信息
        ],
    "female":[...], //省略女性同男性数据
    "common":[...]  //省略通用性别数据
}
{% endhighlight %}

按分组获取角色,大头贴素材
----------------

地址:`/v1/{app_id}/materials/role/group/{groupid}`
地址:`/v1/{app_id}/materials/emoticon/group/{groupid}`

方法:`GET`

说明:当autoversion不传递,或者传递的值不等于服务器那里此分组版本号时,将返回此分组所有的角色或大头贴素材内容

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| auto_version   |float  |素材分组版本号, 例如1.2，1.8等       |否 |

返回值 - 无缓存:
{% highlight js %}
{
        "auto_version": 1.0, //此分组版本号
        "custom_key_value": "{}", //自定义kv字段，json格式字符串
        "custom_tags": "[]", //自定义tag字段，json格式字符串
        "ename": "此分组英文短名",
        "gender": 1, //1表示男性
        "locale_ename": "chn", //分组的主要所属国际化
        "locales":["chn"],        //一个分组所属多个国家预留
        "groups": [
            {
                "auto_version": 1.0, //此分组版本号
                "custom_key_value": "{}", //自定义kv字段，json格式字符串
                "custom_tags": "[]", //自定义tag字段，json格式字符串
                "ename": "此分组英文短名",
                "gender": 1, //1表示男性
                "groups": [...],//支持嵌套，可能有N级
                "materials":[...],//省略此分组下的素材
                "icon_url": "分组图标地址",
                "id": 1,
                "intro": "分组简介",
                "name": "分组名称",
                "parent_group_id": 0,//父分组id
                "sort": 1, //排序
                "type": 1  //1表示角色使用，2表示大头贴使用，3表示通用

            }, //...省略多个子分组
        ],
        "materials": [
                {
                    "custom_key_value": "11",
                    "custom_tags": "11",
                    "ename": "aa1",
                    "id": 1,
                    "img_url_1":"动态表情素材图片地址，nie.1图片",
                    "img_url_2":"动态表情素材图片地址，nie.2图片",
                    "img_url_3":"动态表情素材图片地址，nie.3图片",
                    "img_url_4":"动态表情素材图片地址，nie.4图片",
                    "img_url_5":"动态表情素材图片地址，缩略图用",
                    "is_animation": true,
                    "name": "aa",
                    "sort": 1,
                    "locales":["chn", "jpn"],        //一个素材所属多个国家
                }, ...//省略此分组下的多个素材
        ],
        "icon_url": "分组图标地址",
        "id": 1,
        "intro": "分组简介",
        "name": "分组名称",
        "parent_group_id": 0,//父分组id
        "sort": 1, //排序
        "test": false, //此素材分组是否为测试用
        "type": 1  //1表示角色使用，2表示大头贴使用，3表示通用
}
{% endhighlight %}

返回值 - 有缓存,版本号匹配
{% highlight js %}
{
    "cache":true
}
{% endhighlight %}

获取动态表情素材分组与素材
----------------

地址:`/v1/{app_id}/materials/expressions`

方法:`GET`

说明:此接口没有缓存,用来初始化第一次安装

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| group_only    |Boolean |如果为`1`,则只返回分组信息,如果为`0`则返回全部，默认为`0`   |否 |

返回值:
{% highlight js %}
[
    {
        "id":222, //动态表情素材分组的id
        "name":"动态表情素材分组的名称",
        "ename":"动态表情素材分组的英文短名称",
        "intro":"动态表情素材分组的简介",
        "icon_url":"动态表情素材分组的封面图片",
        "gender":2, //0表示女性，1表示男性，2表示通用,目前动态表情素材没有分男女
        "parent_group_id":0, //目前动态表情这个字段为0,分组没有嵌套
        "custom_key_value":"{key:val}" //管理员自定义kv属性,json格式
        "custom_tags":"['tag1', 'tag2']" //管理员自定义tag属性,json格式
        "auto_version":"动态表情素材分组的版本号",
        "sort":1 //排序,越大排越前面,
        "locale_ename": "chn", //分组的主要所属国际化
        "locales":[],        //一个分组所属多个国家预留,目前动态表情这里都是空
        "test": false, //此素材分组是否为测试用
        "facials":[
            {
                "id":333 //动态表情素材ID
                "ename":"动态表情素材的英文短名称",
                "name":"动态表情素材名称",
                "img_url_1":"动态表情素材图片地址，front的图片",
                "img_url_2":"动态表情素材图片地址，body的图片",
                "img_url_3":"动态表情素材图片地址，back的图片",
                "img_url_4":"动态表情素材图片地址，预留备用",
                "img_url_5":"动态表情素材图片地址，预留备用",
                "is_animation":"是否是动画",
                "custom_key_value":"{key:val}" //管理员自定义kv属性,json格式
                "custom_tags":"['tag1', 'tag2']" //管理员自定义tag属性,json格式
                "sort":1 //排序,越大排越前面
                "locales":[],        //一个分组所属多个国家预留,目前动态表情这里都是空
            }, ...
        ]
    }, ...
]
{% endhighlight %}

按分组获取动态表情素材
----------------

地址:`/v1/{app_id}/materials/expression/group/{groupid}`

方法:`GET`

说明:当autoversion不传递,或者传递的值不等于服务器那里此分组版本号时,将返回此分组所有的表情材料内容

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| auto_version   |String  |素材分组版本号                          |否 |


返回值 - 无缓存:
{% highlight js %}
{
        "id":222, //动态表情素材分组的id
        "name":"动态表情素材分组的名称",
        "ename":"动态表情素材分组的英文短名称",
        "intro":"动态表情素材分组的简介",
        "icon_url":"动态表情素材分组的封面图片",
        "gender":2, //0表示女性，1表示男性，2表示通用,目前动态表情素材没有分男女
        "parent_group_id":0, //目前动态表情这个字段为0,分组没有嵌套
        "custom_key_value":"{key:val}" //管理员自定义kv属性,json格式
        "custom_tags":"['tag1', 'tag2']" //管理员自定义tag属性,json格式
        "auto_version":"动态表情素材分组的版本号",
        "sort":1 //排序,越大排越前面
        "locale_ename": "chn", //分组的主要所属国际化
        "locales":[],        //一个分组所属多个国家预留,目前动态表情这里都是空
        "test": false, //此素材分组是否为测试用
        "facials":[
            {
                "id":333 //动态表情素材ID
                "ename":"动态表情素材的英文短名称",
                "name":"动态表情素材名称",
                "img_url_1":"动态表情素材图片地址，front的图片",
                "img_url_2":"动态表情素材图片地址，body的图片",
                "img_url_3":"动态表情素材图片地址，back的图片",
                "img_url_4":"动态表情素材图片地址，预留备用",
                "img_url_5":"动态表情素材图片地址，预留备用",
                "is_animation":"是否是动画",
                "custom_key_value":"{key:val}" //管理员自定义kv属性,json格式
                "custom_tags":"['tag1', 'tag2']" //管理员自定义tag属性,json格式
                "sort":1 //排序,越大排越前面
                "locales":[],        //一个分组所属多个国家预留,目前动态表情这里都是空
            }, ...
        ]
    }
{% endhighlight %}

返回值 - 有缓存,版本号匹配
{% highlight js %}
{
    "cache":true
}
{% endhighlight %}