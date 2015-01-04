---
layout: page
title: App接入指南
nav-index: 1
---

文档中, App表示客户端,Server表示服务器端

接入步骤
----------------
1. 启动App  
2. App本地判断是否已经在`Server`端注册过, 如果没有注册过,则`Server`返回一个`app_id`和`app_secret`作为身份和加密串,如果无特殊说明`App`每次请求`Server`都必须在路径参数里带上`app_id`作为身份标识,另外`query`参数必须传输`timestamp`时间戳参数作为动态签名用,每次请求`Server`都将带有`sign`签名参数,`Server`根据`sign`来判断此`App`请求是否合法。

`Sign`签名参数生成规则:  
将所传递参数的key根据字典排序,然后将`key`和`value`字符串想加起来,将最终的字符串`md5`哈希得到`sign`签名  

`timestamp`参数（以`秒`为单位的`Int`类型,时区为GMT格林威治当地时间）：
例如: 使用 `moment.js`的话，正确的`timestamp`计算方式应该为
{% highlight javascript %}
var offset = -8; // 西八区为-8,东八区为8，以此类推
var timestamp = moment().format('X') + offset*60*60;
{% endhighlight %}
为了防止重放攻击，客户端每次请求都需要带上`timestamp`参数，服务器会进行判断此参数是否在当前服务器时间前后10分钟范围内

请求示例
----------------

例如用户`post`登录接口,参数如下：

    mobile=13333333333&password=123456&timestamp=1417655951

1.先根据字典将`key`排序,`mobile,password,timestamp`

2.拼接字符串

    string str =
    "mobile1333333333password123456timestamp1417655951"+app_secret

3.对生成的`str`进行`md5`哈希`string sign = toupper(md5(str))`

4.将`sign`参数作为签名参数传给`Server`,`Server`获取到所有参数,将sign签名排除之后用同样的方法声称`sign`来验证。如果合法则继续操作流程,测试环境可暂时不加这个限制,但是功能要预留。

6.`http`接口如不特殊说明,都表示`App`向`Server`请求,如不特殊说明,请求都将带有`sign`,`app_id`和`timestamp`。

6.1、如果获取失败,响应格式为(例如):
{% highlight js %}
{
    "status":"fail",
    "code":1001,
    "result":"数据库连接失败"
}
{% endhighlight %}

6.2、如果获取成功,响应格式为：
{% highlight js %}
{
     "status":"success",
     "code":200,
     "result":"{data}" //不同接口返回的data不同
}
{% endhighlight %}

特别说明
----------------

后续文档中的返回值都表示响应成功里的`result`属性值,如没有特殊说明,接口写到的参数都为必传,并且都需要时间戳`timestamp`和签名`sign`。
所有接口中传递的参数,请求`url`地址、请求参数key和返回值的`key`都约定为纯小写。
