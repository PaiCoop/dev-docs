
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

Promise对象。

#### statusObj

```json
{
	"status": <boolean>, //执行状态，true为成功，false为失败
	"statusCode": <number>, //状态码
	"message": <string>, //提示信息
	"pos": <Array> //显示错误的位置
}
```
| 状态码 | 描述 |
| :--: | :--: |
| 0 | 成功 |
| 3xx | 无法连接到服务器 |
| 4xx | 参数不完整或格式错误 |
| 5xx | 服务器错误 |



### e.g.

```js
//正确格式
;(async function(){
	try{
		console.log('good---->', await sdk.push({
		    "version": 0.1,
		    "userProfile": {
		        "netid": "yimian.liu17",
		        "domain": "student.xjtlu.edu.cn",
		        "email": ["i@yimian.xyz"],
		        "nickname": "iotcat",
		        "gender": "male"
		    },
		    "userPreference": {
		        "anonymous": false,
		        "notify": true
		    },
		    "meta": {
		        "graduateYear": 2021,
		        "department": "Electrical & Electronic Engineering",
		        "major": "Electronic Science Techonology",
		        "2plus2": true,
		        "grade": {
		            "year2": 84,
		            "year1": 80,
		            "year0": 74,
		            "gpa": 3.83,
		            "majorGpa": 3.99,
		            "rank": undefined,
		            "no1Grade": undefined,
		            "scholarship": "full"
		        },
		        "language": [],
		        "tests": [],
		        "internships": [{
		            "title": "IETE欧朗物联",
		            "type": ["iete", "foreign"],
		            "length": 60,
		            "relavence": 10,
		            "gain": 9.6
		        }],
		        "projects": [{
		            "title": "智慧农业",
		            "type": ["surf", "university"],
		            "length": 60,
		            "relavence": 10,
		            "gain": 6.8
		        }, {
		            "type": ["diy"],
		            "length": 358,
		            "relavence": 9.2,
		            "gain": 8.6
		        }],
		        "papers": [],
		        "competitions": [{
		            "relavence": 6.7,
		            "contribution": 4.5,
		            "value": 3.2
		        }],
		        "clubs": [{
		            "title": "infoco",
		            "relavence": 7.6,
		            "value": 6.4,
		            "contribution": 1
		        }],
		        "agent":{},
		        "applications": [{
		            "country": "us",
		            "university": "Cornell university",
		            "department": "Electrical and Computer Engineering",
		            "major": "Electrical and Computer Engineering",
		            "degree": "MEng",
		            "referenceContribution": 9,
		            "applicationDate": "2021-01-04",
		            "applicationEndDate": "2021-03-09",
		            "status": "adimitted"
		        }, {
		            "country": "uk",
		            "university": "university College London",
		            "department": "Electrical and Electronic Engineering",
		            "major": "Integrated Machine Learning Systems",
		            "degree": "MSc",
		            "referenceContribution": 6,
		            "applicationDate": "2021-11-21",
		            "applicationEndDate": "2021-02-14",
		            "status": "adimitted"
		        }, {
		            "country": "us",
		            "university": "Duke University",
		            "department": "Electrical and Computer Engineering",
		            "major": "Electrical and Computer Engineering",
		            "degree": "MSc",
		            "referenceContribution": 4,
		            "applicationDate": "2021-01-14",
		            "applicationEndDate": "2021-02-03",
		            "status": "adimitted"
		        }, {
		            "country": "uk",
		            "university": "University of Edinburgh",
		            "department": "Informatics",
		            "major": "Computer Science",
		            "degree": "MSc",
		            "referenceContribution": 9,
		            "applicationDate": "2021-11-29",
		            "applicationEndDate": "2021-05-02",
		            "status": "adimitted"
		        }, {
		            "country": "uk",
		            "university": "University of Edinburgh",
		            "department": "Informatics",
		            "major": "Informatics",
		            "degree": "MSc",
		            "referenceContribution": 9,
		            "applicationDate": "2021-12-03",
		            "applicationEndDate": "2021-05-18",
		            "status": "adimitted"
		        }],
		        "decision": 0
		    },
		    "article": {
		        "format": "markdown",
		        "data": "肥肠肥肠长的经验分享文~~~"
		    },
		    "feedback": {}
		}));
	}catch(e){
		console.log('err-----> ', e)
	}
})()
````

```js
//错误格式
;(async function(){
	try{
		console.log('good------>', await sdk.push({
			version: 0.1
		}));
	}catch(e){
		console.log('err-----> ', e)
	}
})()
```

## 获取表单

### Syntax

```js
sdk.pull(String netid)
```

### Parameters

 - `netid`: 西浦id。

### Returns

Promise对象。

### e.g. 

```js
;(async function(){
	console.log(await sdk.pull('yimian.liu17'));
})()
````


## 重置(仅测试目的)

删除所有数据。

### Syntax

```js
sdk.reset()
```

### e.g.

```js
sdk.reset();
```


## 获取列表

### Syntax

```js
sdk.getList()
```

### Returns

Promise对象。

### e.g.

```js
;(async function(){
	console.log(await sdk.getList());
})()
```





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