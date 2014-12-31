User Basic
================
用户基本接口

用户登录
----------------

地址:`/user/login`

方法:`POST`  

说明:`cellphone`和`username`两个参数传递其中之一即可,优先`cellphone`  

参数:  

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| cellphone     |String  |用户手机号码                       |*见说明|
| username      |String  |用户名                            |*见说明|
| password      |String  |密码                              |*是   |
| logincode1      |String  |登录推广标识1                     |否   |
| logincode1      |String  |登录推广标识2                     |否   |

返回值:  
```json
{
    "logintoken":"abcdefg", //以后可以通过loginToken参数来标识用户已经登录后的身份
    "userid":111,
    "cellphone":"13333333333",
    "isvalidphone":"isvalidphone", //手机是否已经验证
    "username":"username",
    "nickname":"nickname",
    "gender":0,
    "email":"xxx@xxx.com",
    "pwdquestion1":"pwdQuestion1",//如果用户未设置,此处是null
    "pwdquestion2":"pwdQuestion2",//如果用户未设置,此处是null
    "defaultavatar":"defaultavatar"//用户选择默认的头像
}
```

用户注册
----------------

地址:`/user/register`  

方法:`POST`  

说明:  
`cellphone`和`username`两个参数传递其中之一即可,优先`cellphone`  
如果用户上传了smssign短信验证,并且验证成功,则用户就成为了手机认证用户,可以用过手机号找回密码  

参数:  

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| cellphone     |String  |用户手机号码                       |*见说明|
| username      |String  |用户名                            |*见说明|
| password      |String  |密码                              |*是   |
| smssign       |String  |短信验证码                         |否   |
| nickname      |String  |用户昵称                           |否   |
| gender        |Integer |0表示女性,1表示男性                 |否   |
| email         |String  |用户邮箱                           |否   |
| attributes    |String  |用户推广标识属性                    |否   |
| pwdquestion1  |String  |密保问题1                          |否   |
| pwdanwser1    |String  |密保问题答案1                      |否   |
| pwdquestion2  |String  |密保问题2                          |否   |
| pwdanswer2    |String  |密保问题答案2                       |否   |

返回值:
```json
{
    "logintoken":"abcdefg", //以后可以通过loginToken参数来标识用户已经登录后的身份
    "userid":111,
    "cellphone":"13333333333",
    "isvalidphone":"isvalidphone", //手机是否已经验证
    "username":"username",
    "nickname":"nickname",
    "gender":0,
    "email":"xxx@xxx.com",
    "pwdquestion1":"pwdQuestion1",
    "pwdquestion2":"pwdQuestion2",
    "defaultavatar":"defaultavatar",//用户选择默认的头像
}
```

手机找回密码
----------------

地址:`/user/forgot/cellphone/`

方法:`POST`

说明:无

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| cellphone     |String  |手机号码                           |*是  | 
| smssign       |String  |短信验证码                         |*是   |
| newpassword   |String  |用户需要修改的新密码                 |*是   |

返回值:
```json
{}
```

密保问题找回密码
----------------

地址:`/user/forgot/pwdquestion/`

方法:`POST`

说明:`cellphone`和`username`两个参数传递其中之一即可,优先cellphone

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| cellphone     |String  |手机号码                           |*见说明| 
| username      |String  |用户名                             |*见说明|
| pwdanwser1    |String  |密保问题答案1                      |*是   |
| pwdanwser2    |String  |密保问题答案1                      |*是   |
| newpassword   |String  |用户需要修改的新密码                 |*是   |

返回值:
```json
{}
```

获取密保问题
----------------

地址:`/user/pwdquestions/`

方法:`GET`

说明:`cellphone`和`username`两个参数传递其中之一即可,优先cellphone

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| cellphone     |String  |手机号码                           |*见说明| 
| username      |String  |用户名                             |*见说明|

返回值:
```json
{
     "pwdquestion1":"pwdquestion1",
     "pwdquestion1":"pwdquestion2",
}
```

绑定第三方账户
----------------

地址:`/user/socialbind`

方法:`POST`

说明:无

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| logintoken     |String  |用户登录令牌识别码                    |*是 |  
| "provider"       |Enum    |第三方提供商 (QQ,微信,微博,Facebook等)|*是 |
| "openid"         |String  |用户在第三方提供商的"openid"            |*是 |
| accesstoken    |String  |用户在第三方提供商的Access Token      |否 |
| refreshtoken   |String  |用户在第三方提供商的Refresh Token     |否 |

返回值:
```json
{}
```

获取已绑定第三方账户列表
----------------

地址:`/user/socialbinds`

方法:`GET`

说明:无

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----| 
| logintoken     |String  |用户登录令牌识别码                    |*是 |  

返回值:
```json
[
    {
        "provider":"weixin",//(枚举字符串,'weixin', 'qq', 'weibo')
        "openid":"openid"
    },
    {
        "provider":"qq",//(枚举字符串,'weixin', 'qq', 'weibo')
        "openid":"openid"
    },
    {
        "provider":"weibo",//(枚举字符串,'weixin', 'qq', 'weibo')
        "openid":"openid"
    }
]
```

获取详细信息
----------------

地址:`/user/profile`

方法:`GET`

说明:无

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| logintoken     |String  |用户登录令牌识别码                    |*是 | 

返回值:
```json
{
    "userid":111,
    "cellphone":"13333333333",
    "username":"username",
    "nickname":"nickname",
    "gender":0,
    "email":"xxx@xxx.com",
    "pwdquestion1":"pwdQuestion1",
    "pwdquestion2":"pwdQuestion2",
    "defaultemoticon":"defaultemoticon"
}
```

修改详细信息
----------------

地址:`/user/profile`

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
```json
{
    "nickname":"nickname",
    "gender":0,
    "email":"xxx@xxx.com",
    "pwdquestion1":"pwdQuestion1",
    "pwdquestion2":"pwdQuestion2"
}
```

绑定手机
----------------

地址:`/user/bindphone`

方法:`POST`

说明:无

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----| 
| logintoken     |String  |用户登录令牌识别码                    |*是 |
| cellphone      |String  |用户手机号码                         |*是 |
| smssign        |String  |短信验证码                           |*是 |

返回值:
```json
{}
```

验证密保问题
----------------

地址:`/user/pwdquestion/validate`

方法:`POST`

说明:无

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| logintoken     |String  |用户登录令牌识别码                    |*是 |
| pwdanswer1     |String  |密保问题1答案                        |*是 |
| pwdanswer2     |String  |密保问题2答案                        |*是 |

返回值:
```json
{}
```

修改密保问题
----------------

地址:`/user/pwdquestion/update`

方法:`POST`

说明:无

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----| 
| logintoken     |String  |用户登录令牌识别码                           |*是 |
| oldpwdanswer1  |String  |旧密保问题1答案(如果用户第一次设置密保问题,留空)  |*是 |
| oldpwdanswer2  |String  |旧密保问题2答案(如果用户第一次设置密保问题,留空)  |*是 |
| pwdquestion1   |String  |新密保问题1                                  |*是 |
| pwdanwser1     |String  |新密保问题答案1                              |*是 |
| pwdquestion2   |String  |新密保问题2                                  |*是 |
| pwdanswer2     |String  |新密保问题答案2                               |*是 |

返回值:
```json
{}
```

修改密码
----------------

地址:`/user/changepassword`

方法:`POST`

说明:无

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----| 
| logintoken     |String  |用户登录令牌识别码                   |*是 |
| oldpassword    |String  |旧密码                             |*是 |
| password       |String  |新密码                             |*是 |

返回值:
```json
{}
```

获取用户留言列表
----------------

地址:`/user/messages`

方法:`GET`

说明:无

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| ename          |String  |应用ename                          |*是 | 
| logintoken     |String  |用户登录令牌识别码                   |*是 |

返回值:
```json
[
    {
        "id":123,
        "userid":133,
        "title":"提点意见",
        "message":"能否多几套动态表情供选择呢",
        "reply":"我们已经接受采纳,新版本会新增2套全新动态表情,谢谢反馈",
        "write_time":"2014/11/22 11:11",
        "update_time":"2014/11/22 11:11",
    }
    // ... 
]
```

用户留言
----------------

地址:`/user/message/add`

方法:`POST`

说明:无

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| ename          |String  |应用ename                          |*是 | 
| logintoken     |String  |用户登录令牌识别码                   |*是 |
| title          |String  |用户留言标题                        |*是 |
| message        |String  |用户留言内容                        |*是 |

返回值:
```json
{}
```
