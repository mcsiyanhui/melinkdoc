Auth 
================
App认证授权相关接口

设备注册
----------------
App向Server注册设备,获取appid和appkey

地址: `/v1/app/register`

方法: `GET`

说明: 不需要`sign`签名,不需要传`appid`,`sign`,`timestamp`参数

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| ename         |String  |平台将根据ename来判断是否此应用授权接入|*是   |
| primary_from  |String  |此App主要安装推广标识               |否   |
| secondary_from|String  |此App次要安装推广标识               |否   |

返回值:
```json
{
    "app_id":"123456",
    "app_secret":"123456"
}
```

获取版本号
----------------

地址:`/v1/app/version"`

方法:`GET`

说明: 不需要`sign`签名,不需要传`appid`,`sign`,`timestamp`参数

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| ename         |String  |平台将根据ename来识别接入应用        |*是   |


返回值:
```json
{
    "intro":"app介绍",
    "apple_version":"1.0",
    "android_version":"1.0",
    "android_version2":"1.0",
    "force_vpdate":true,
    "update_url":"http://www.baidu.com",
    "cover_img":"http://www.baidu.com",  //启动页面url地址
    "weibo_url":"http://www.baidu.com",  //微博的推广地址
    "weixin_url":"http://www.baidu.com", //微信的推广地址
}
```

获取手机验证码
----------------

地址:`/v1/{appid}/app/sms"/{mobile}`

方法:`GET`

说明:需要签名

参数:

| url参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| mobile        |String  |需要获取验证码的手机号码             |*是   |

返回值:

    {}
