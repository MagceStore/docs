# API 设计规范
#### Version 1.0

## HTTP状态规范
* 系统框架返回`400`, `401`, `403`, `404`, `500`状态码
* 数据验证，业务逻辑错误等需要通知给客户端，均返回`499`状态码
* 服务器端未知错误，需返回`500`状态码
* 成功均返回`200`状态码


## 错误信息数据结构
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
  "code": 1001,
  "message": "Token 不正确",
  "fields": [{
    "field": "name",
    "message": "超过20个字符"
  }]
}
```
