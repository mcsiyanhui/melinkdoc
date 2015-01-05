---
layout: page
title: 用户基本接口
nav-index: 3
---
用户基本接口

用户登录
----------------

地址:`/v1/{app_id}/user/login`

方法:`POST`  

说明:`cellphone`和`username`两个参数传递其中之一即可,优先`cellphone`  

参数:  

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| cellphone     |String  |用户手机号码                       |*见说明|
| username      |String  |用户名                            |*见说明|
| password      |String  |密码                              |*是   |
| from1      |String  |登录推广来源标识1                     |否   |
| from2      |String  |登录推广来源标识2                     |否   |

返回值:  
{% highlight js %}
{
    "logintoken":"abcdefg", //以后可以通过loginToken参数来标识用户已经登录后的身份
    "user_id":111,
    "cellphone":"13333333333",
    "isvalid_phone":"isvalidphone", //手机是否已经验证
    "username":"username",
    "nickname":"nickname",
    "gender":0,
    "email":"xxx@xxx.com",
    "pwd_question1":"pwdQuestion1",//如果用户未设置,此处是null
    "pwd_question2":"pwdQuestion2",//如果用户未设置,此处是null
    "default_emoticon":"defaultavatar",//用户选择默认的大头贴
    "isvalid_phone":true//用户是否绑定手机
}
{% endhighlight %}

用户注册
----------------

地址:`/v1/{app_id}/user/register`

方法:`POST`  

说明:  
`cellphone`和`username`两个参数传递其中之一即可,优先`cellphone`  
如果用户上传了`sms_sign`短信验证,并且验证成功,则用户就成为了手机认证用户,可以用过手机号找回密码

参数:  

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| cellphone     |String  |用户手机号码                       |*见说明|
| username      |String  |用户名                            |*见说明|
| password      |String  |密码                              |*是   |
| sms_sign       |String  |短信验证码                         |否   |
| nickname      |String  |用户昵称                           |否   |
| gender        |Integer |0表示女性,1表示男性                 |否   |
| email         |String  |用户邮箱                           |否   |
| from1         |String  |用户推广来源标识属性1                    |否   |
| from2         |String  |用户推广来源标识属性2                    |否   |
| pwd_question1  |String  |密保问题1                          |否   |
| pwd_anwser1    |String  |密保问题答案1                      |否   |
| pwd_question2  |String  |密保问题2                          |否   |
| pwd_answer2    |String  |密保问题答案2                       |否   |

返回值:
{% highlight js %}
{
    "logintoken":"abcdefg", //以后可以通过loginToken参数来标识用户已经登录后的身份
    "user_id":111,
    "cellphone":"13333333333",
    "isvalid_phone":true, //手机是否已经验证
    "username":"username",
    "nickname":"nickname",
    "gender":0,
    "email":"xxx@xxx.com",
    "pwd_question1":"pwdQuestion1",
    "pwd_question2":"pwdQuestion2",
    "default_emoticon":"defaultavatar",//用户选择默认的头像
}
{% endhighlight %}

手机找回密码
----------------

地址:`/v1/{app_id}/user/forgot/cellphone`

方法:`POST`

说明:无

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| cellphone     |String  |手机号码                           |*是  | 
| sms_sign       |String  |短信验证码                         |*是   |
| new_password   |String  |用户需要修改的新密码                 |*是   |

返回值:
{% highlight js %}
{}
{% endhighlight %}

密保问题找回密码
----------------

地址:`/v1/{app_id}/user/forgot/pwdquestion"`

方法:`POST`

说明:`cellphone`和`username`两个参数传递其中之一即可,优先cellphone

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| cellphone     |String  |手机号码                           |*见说明| 
| username      |String  |用户名                             |*见说明|
| pwd_anwser1    |String  |密保问题答案1                      |*是   |
| pwd_anwser2    |String  |密保问题答案1                      |*是   |
| new_password   |String  |用户需要修改的新密码                 |*是   |

返回值:
{% highlight js %}
{}
{% endhighlight %}

获取密保问题
----------------

地址:`/v1/{app_id}/user/forgot/pwdquestion`

方法:`GET`

说明:`cellphone`和`username`两个参数传递其中之一即可,优先cellphone

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| cellphone     |String  |手机号码                           |*见说明| 
| username      |String  |用户名                             |*见说明|

返回值:
{% highlight js %}
{
     "pwd_question1":"pwdquestion1",
     "pwd_question2":"pwdquestion2",
}
{% endhighlight %}


用户通过第三方账户登录
----------------

地址:`/v1/{app_id}/user/sociallogin`

方法:`POST`

说明:app应用先调用这个接口，当返回失败，再提示用户绑定或者注册表情me帐号，调用下面`绑定第三方账户`进行绑定操作

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| provider       |Enum [qq,weibo,weixin]    |第三方提供商 (QQ,微信,微博,Facebook等)|*是 |
| openid         |String  |用户在第三方提供商的"openid"            |*是 |
| login_code1      |String  |登录推广标识1                     |否   |
| login_code2      |String  |登录推广标识2                     |否   |

返回值:
{% highlight js %}
{
    "logintoken":"abcdefg", //以后可以通过loginToken参数来标识用户已经登录后的身份
    "user_id":111,
    "cellphone":"13333333333",
    "isvalid_phone":"isvalidphone", //手机是否已经验证
    "username":"username",
    "nickname":"nickname",
    "gender":0,
    "email":"xxx@xxx.com",
    "pwd_question1":"pwdQuestion1",//如果用户未设置,此处是null
    "pwd_question2":"pwdQuestion2",//如果用户未设置,此处是null
    "default_emoticon":"defaultavatar",//用户选择默认的大头贴
    "isvalid_phone":true//用户是否绑定手机
}
{% endhighlight %}


绑定第三方账户
----------------

地址:`/v1/{app_id}/user/socialbind`

方法:`POST`

说明:无

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| logintoken     |String  |用户登录令牌识别码                    |*是 |  
| provider       |Enum [qq,weibo,weixin]    |第三方提供商 (QQ,微信,微博,Facebook等)|*是 |
| openid         |String  |用户在第三方提供商的"openid"            |*是 |
| avatar    |String  |用户在第三方的头像      |否 |
| nickname    |String  |用户在第三方的昵称      |否 |
| accesstoken    |String  |用户在第三方提供商的Access Token      |否 |
| refreshtoken   |String  |用户在第三方提供商的Refresh Token     |否 |

返回值:
{% highlight js %}
{}
{% endhighlight %}

获取已绑定第三方账户列表
----------------

地址:`/v1/{app_id}/user/socialbind`

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
        "provider":"weixin",//(枚举字符串,'weixin', 'qq', 'weibo')
        "openid":"openid",
        "avatar":"avatar",
        "nickname":"nickname"
    },
    {
        "provider":"qq",//(枚举字符串,'weixin', 'qq', 'weibo')
        "openid":"openid",
        "avatar":"avatar",
        "nickname":"nickname"
    },
    {
        "provider":"weibo",//(枚举字符串,'weixin', 'qq', 'weibo')
        "openid":"openid",
        "avatar":"avatar",
        "nickname":"nickname"
    }
]
{% endhighlight %}

获取详细信息
----------------

地址:`/v1/{app_id}/user/profile`

方法:`GET`

说明:无

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| logintoken     |String  |用户登录令牌识别码                    |*是 | 

返回值:
{% highlight js %}
{
    "user_id":111,
    "cellphone":"13333333333",
    "username":"username",
    "nickname":"nickname",
    "gender":0,
    "email":"xxx@xxx.com",
    "pwd_question1":"pwdQuestion1",
    "pwd_question2":"pwdQuestion2",
    "default_emoticon":"defaultemoticon"
}
{% endhighlight %}

修改详细信息
----------------

地址:`/v1/{app_id}/user/profile"`

方法:`POST`

说明:无

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----| 
| logintoken     |String  |用户登录令牌识别码                    |*是 |
| nickname       |String  |用户昵称                            |否 |
| gender         |Integer |用户性别                            |否 |
| email          |String  |用户邮箱                            |否 |

返回值:
{% highlight js %}
{
    "nickname":"nickname",
    "gender":0,
    "email":"xxx@xxx.com"
}
{% endhighlight %}

绑定手机
----------------

地址:`/v1/{app_id}/user/bindphone"`

方法:`POST`

说明:无

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----| 
| logintoken     |String  |用户登录令牌识别码                    |*是 |
| cellphone      |String  |用户手机号码                         |*是 |
| sms_sign        |String  |短信验证码                           |*是 |

返回值:
{% highlight js %}
{}
{% endhighlight %}

验证密保问题
----------------

地址:`/v1/{app_id}/user/pwdquestion/validate`

方法:`POST`

说明:无

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| logintoken     |String  |用户登录令牌识别码                    |*是 |
| pwd_answer1     |String  |密保问题1答案                        |*是 |
| pwd_answer2     |String  |密保问题2答案                        |*是 |

返回值:
{% highlight js %}
{}
{% endhighlight %}

修改密保问题
----------------

地址:`/v1/{app_id}/user/pwdquestion/update`

方法:`POST`

说明:无

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----| 
| logintoken     |String  |用户登录令牌识别码                           |*是 |
| old_pwd_answer1  |String  |旧密保问题1答案(如果用户第一次设置密保问题,留空)  |*是 |
| old_pwd_answer2  |String  |旧密保问题2答案(如果用户第一次设置密保问题,留空)  |*是 |
| pwd_question1   |String  |新密保问题1                                  |*是 |
| pwd_anwser1     |String  |新密保问题答案1                              |*是 |
| pwd_question2   |String  |新密保问题2                                  |*是 |
| pwd_answer2     |String  |新密保问题答案2                               |*是 |

返回值:
{% highlight js %}
{}
{% endhighlight %}

修改密码
----------------

地址:`/v1/{app_id}/user/changepassword`

方法:`POST`

说明:无

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----| 
| logintoken     |String  |用户登录令牌识别码                   |*是 |
| old_password    |String  |旧密码                             |*是 |
| password       |String  |新密码                             |*是 |

返回值:
{% highlight js %}
{}
{% endhighlight %}

获取用户留言列表
----------------

地址:`/v1/{app_id}/user/messages`

方法:`GET`

说明:无

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| logintoken     |String  |用户登录令牌识别码                   |*是 |

返回值:
{% highlight js %}
[
    {
        "id":123,
        "title":"提点意见",
        "message":"能否多几套动态表情供选择呢",
        "reply":"我们已经接受采纳,新版本会新增2套全新动态表情,谢谢反馈",
        "write_time":"2014/11/22 11:11",
        "update_time":"2014/11/22 11:11"
    }
    // ... 
]
{% endhighlight %}

用户留言
----------------

地址:`/v1/{app_id}/user/messages`

方法:`POST`

说明:无

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| logintoken     |String  |用户登录令牌识别码                   |*是 |
| title          |String  |用户留言标题                        |*是 |
| message        |String  |用户留言内容                        |*是 |

返回值:
{% highlight js %}
{}
{% endhighlight %}
