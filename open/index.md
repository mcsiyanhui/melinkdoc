---
layout: page
title: 开放接口
nav-index: 8
---
对外开放数据接口

接口根路径
----------------
**RootURL**: openapi.domain.com/{v1}

获取用户默认角色
----------------

地址:`/v1/user/emoticon/{username}`

方法:`GET`

说明:`{username}`表示此用户的用户名

参数:

     无

返回值:

     302跳转，跳转到七牛返回二进制图片，此用户设置的对外的默认角色


获取用户默认表情
----------------

地址:`/v1/user/expression/{username}`

方法:`GET`

说明:`{username}`表示此用户的用户名

参数:

     无

返回值:

     02跳转，跳转到七牛返回二进制图片，此用户设置的对外的默认表情