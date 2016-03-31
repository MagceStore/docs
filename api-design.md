# API 设计规范
#### Version 1.0

## HTTP状态码规范
* 系统框架返回`400`, `401`, `403`, `404`, `500`状态码
* 数据验证，业务逻辑错误等需要通知给客户端，均返回`499`状态码
* 服务器端未知错误，需返回`500`状态码
* 成功均返回`200`状态码

## Response 错误信息数据结构
#### <a name="errorResponseObject"></a>Error Response Object

Field Name | Type | Description
---|:---:|---
code | integer | 错误代码
message | string | 错误描述
fields | [[Validated Error Object](#validatedErrorObject)] | 当有数据验证错误时，此字段会出现

#### <a name="validatedErrorObject"></a>Validated Error Object
Field Name | Type | Description
---|:---:|---
filed | string | 字段名
message | string | 错误描述

```js
{
  "code": 1001,
  "message": "Token 不正确"
}
```

```js
{
  "code": 2000,
  "message": "数据验证错误",
  "fields": [{
    "field": "name",
    "message": "超过20个字符"
  }]
}
```

## Response 分页数据结构

Filed Name | Type | Description
---|:---:|---
items | [Object] | 数据
\_links | Object | 当前页链接
\_meta | [Pagination Meta Object](#metaObject) | 分页数据

#### <a name="metaObject"></a>Pagination Meta Object
Filed Name | Type | Description
---|:---:|---
totalCount | integer | 总记录数
pageCount | integer | 总分页数
currentPage | integer | 当前页码
perPage | integer | 每页记录数

```js
{
  "items": [
    {
      "id": "1",
      "email": "jin.chen@starlight-sms.com",
      "name": "Jin.Chen",
      "status": "ACTIVE"
    },
  ],
  "_links": {
    "self": {
      "href": "http://127.0.0.1:8810/v1/users?page=1"
    },
    "next": {
      "href": "http://127.0.0.1:8810/v1/users?page=2"
    },
    "last": {
      "href": "http://127.0.0.1:8810/v1/users?page=3"
    }
  },
  "_meta": {
    "totalCount": 3,
    "pageCount": 1,
    "currentPage": 1,
    "perPage": 20
  }
}
```

## Response (PUT/POST/GET) 直接返回 Object
