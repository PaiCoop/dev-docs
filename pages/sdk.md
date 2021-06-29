
# 概述

浏览器SDK(Software Development Kit)位于客户端，负责守护客户端与服务端之间的通信，以及对客户端的身份识别。UI可通过调用SDK提供的函数，与服务端进行交互。下文将具体阐述SDK函数的设计。


# 使用

在html中`</body>`前加入下行代码。

```html
<script src="https://cdn.jsdelivr.net/npm/paicoop-browser-sdk"></script>
```

之后初始化SDK。
```html
<script>
sdk = new Paicoop();
</script>
```

然后可以正常调用。


# 业务函数

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
| 状态码 | 描述 |
| :--: | :--: |
| 0 | 成功 |
| 3xx | 无法连接到服务器 |
| 4xx | 参数不完整或格式错误 |
| 5xx | 服务器错误 |

> 当前测试程序尚未完成格式检查功能


## 获取表单

### Syntax

```js
sdk.pull(String netid)
```

### Parameters

 - `netid`: 西浦id。

### Returns

FormObject。如找不到则返回null。


## 获取列表

### Syntax

```js
sdk.getList()
```

### Returns

ListObject





# 业务工具


## 本地数据库

将数据存储到浏览器本地，以便在用户关闭浏览器时保持数据。


### Syntax


```js
sdk.db.set('foo', 'bar'); // store 'bar' value under 'foo' key
sdk.db.set('abc', 'xyz'); // store 'xyz' value under 'abc' key
sdk.db.get('foo'); // returns 'bar'
sdk.db.keys(); // returns ['abc', 'foo']
sdk.db.remove('foo'); // remove 'foo' value
sdk.db.reset(); // reset all stored values
```
更多方法见[basil.js文档](https://github.com/Wisembly/basil.js)。



## 提示框

弹出一个提示框。

### Syntax

```js
sdk.tips
```
`sdk.tips`继承自`iziToast`对象。详见[iziToast手册](https://izitoast.marcelodolza.com/)。

### Examples

```js
sdk.tips.show({
    title: 'Hey',
    message: 'What would you like to add?'
});
```