
# 概述

浏览器SDK(Software Development Kit)位于客户端，负责守护客户端与服务端之间的通信，以及对客户端的身份识别。UI可通过调用SDK提供的函数，与服务端进行交互。下文将具体阐述SDK函数的设计。


# 函数设计

## 提交表单

### Syntax

```js
sdk.push(Object FormObject)
```

### Parameters

 - `FormObject`: 标准表单对象。

### Returns

```json
{
	"status": <boolean>, //执行状态，true为成功，false为失败
	"statusCode": <number>, //状态码
	"message": <string> //提示信息
}
```