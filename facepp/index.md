---
layout: page
title: face++人脸识别
nav-index: 8
---

face++人脸识别

根据用户上传的图片，识别相似明星，返回明显卡通图片
----------------

地址:`/v1/<appid>/star/search`

方法:`POST`

说明:POST图片数据，识别相似明星，返回卡通图片

参数:

| 参数名称        |类型    |说明                              |是否必须|
|:------------- |:-------|:--------------------------------|:-----|
| img_data       |String  |待识别的图片（base64字符串），不参与签名         |*是|
| mime_type    |str |可选参数，`jpg`或`png`，默认为`jpg`   |否 |

返回值:
{% highlight js %}
{
        "id":11,//明星脸记录id
        "name":"范冰冰",//明星的名字
        "gender":"女",//性别
        "intro":"",//简介
        "star_pic1":"http://www.faceplusplus.com.cn/wp-content/themes/faceplusplus/assets/img/demo/thumbnail/1.jpg?v=2",//原始明星头像
        "star_pic2":"http://www.faceplusplus.com.cn/wp-content/themes/faceplusplus/assets/img/demo/thumbnail/1.jpg?v=2",//卡通头像地址
        "star_pic3":"",
        "star_pic4":"",
        "star_pic5":"",
        "user_upload_avatar":"http://www.faceplusplus.com.cn/wp-content/themes/faceplusplus/assets/img/demo/thumbnail/1.jpg?v=2",//用户上传的头像地址
        "role_id":0,       //卡通头像的基础role_id
        "confidence":90.99 //相似度
}
{% endhighlight %}