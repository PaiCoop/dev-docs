
# 概述

浏览器SDK(Software Development Kit)位于客户端，负责守护客户端与服务端之间的通信，以及对客户端的身份识别。UI可通过调用SDK提供的函数，与服务端进行交互。下文将具体阐述SDK函数的设计。


# 使用

## 快速开始

在html中`</body>`前加入下行代码。

```html
<script src="https://cdn.jsdelivr.net/npm/paicoop-browser-sdk"></script>
<script>
sdk = new Paicoop();
</script>
```

然后可以正常调用。


## 进阶

`PaiCoop`构造函数可以接受以下参数。

```js
options = {
		systemNamespace: '__PaiCoop', //本地系统数据库命名空间
		customNamespace: '__Custom', //本地用户数据库命名空间
		host: 'http://cn3.yimian.xyz/api/', //API接口地址
		localMode: false, //本地测试模式
		mask: <MaskObj> //自定义form mask
}
```

以上均为可选参数。请使用类似如下方式使用自定义参数初始化。
```html
<script src="https://cdn.jsdelivr.net/npm/paicoop-browser-sdk"></script>
<script>
sdk = new Paicoop({
	host: 'http://paicoop.net/api/', //使用自定义API地址
	localMode: true //开启本地测试模式
});
</script>
```


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

#### resolve

[status对象](/pages/dictionary?id=statusobj)。例如

```js
{
	status: true, //成功
	statusCode: 0, 
	message: "Successful!",
	data: {
		acknowledged: true, //数据库确认收到
		modifiedCount: 0, //发生改动的数据条目
		upsertedCount: 0,  //新插入的数据条目
		matchedCount: 1, //匹配的原有数据条目
		upsertedId: null
	}
}
```

#### reject

[status对象](/pages/dictionary?id=statusobj)。例如
```js
{
	status: false,
	statusCode: 402,
	message: "Form format error! For details see data.",
	data: [{"userPreference": ["anonymous"]}] //提示form中的userPreference的anonymous有错误
}
```

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

#### resolve

[form对象](/pages/dictionary?id=formobj)。
#### reject

[status对象](/pages/dictionary?id=statusobj)。例如

```js
{
	status: false,
	statusCode: 300,
	message: "Cannot connect to host!",
	data: undefined
}
```



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

#### resolve

[list对象](/pages/dictionary?id=listobj)。
#### reject

[status对象](/pages/dictionary?id=statusobj)。例如

```js
{
	status: false,
	statusCode: 300,
	message: "Cannot connect to host!",
	data: undefined
}
```

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