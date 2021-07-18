# 概述

下文主要陈述服务器提供的应用程序接口(API)规范。


# API

## getList

获取List信息

### 地址

```
GET /getList
```

### 参数

无

### 返回值

[JSON格式status对象](/pages/dictionary?id=statusobj)

#### 示例

```json
{
    "status": true,
    "statusCode": 0,
    "message": "Successful!",
    "data": [
        {
            "netid": "yimian.liu17",
            "nickname": "iotcat",
            "item": {
                "country": "us",
                "university": "Cornell university",
                "department": "Electrical and Computer Engineering",
                "major": "Electrical and Computer Engineering",
                "degree": "MEng",
                "referenceContribution": 9,
                "applicationDate": "2021-01-04",
                "applicationEndDate": "2021-03-09",
                "status": "adimitted",
                "conditions": null
            },
            "meta": {
                "graduateYear": 2021,
                "department": "electrical & electronic engineering",
                "major": "electronic science techonology",
                "2plus2": true,
                "grade": {
                    "year2": 84,
                    "year0": 74,
                    "year1": 80,
                    "year3": null,
                    "gpa": 3.83,
                    "majorGpa": 3.99,
                    "rank": null,
                    "no1Grade": null,
                    "scholarship": "full"
                },
                "language": [],
                "tests": [],
                "internships": [
                    {
                        "title": "IETE欧朗物联",
                        "type": [
                            "iete",
                            "foreign"
                        ],
                        "length": 60,
                        "relavence": 10,
                        "gain": 9.6
                    }
                ],
                "projects": [
                    {
                        "title": "智慧农业",
                        "type": [
                            "surf",
                            "university"
                        ],
                        "length": 60,
                        "relavence": 10,
                        "gain": 6.8
                    },
                    {
                        "title": null,
                        "type": [
                            "diy"
                        ],
                        "length": 358,
                        "relavence": 9.2,
                        "gain": 8.6
                    }
                ],
                "papers": [],
                "competitions": [
                    {
                        "title": null,
                        "relavence": 6.7,
                        "contribution": 4.5,
                        "award": null,
                        "value": 3.2
                    }
                ],
                "clubs": [
                    {
                        "title": "infoco",
                        "relavence": 7.6,
                        "value": 6.4,
                        "contribution": 1
                    }
                ],
                "agent": {
                    "title": null,
                    "plan": null,
                    "overall": null,
                    "knowledge": null,
                    "cvSkill": null,
                    "responsibility": null,
                    "cost": null
                },
                "applications": [
                    {
                        "country": "us",
                        "university": "Cornell university",
                        "department": "Electrical and Computer Engineering",
                        "major": "Electrical and Computer Engineering",
                        "degree": "MEng",
                        "referenceContribution": 9,
                        "applicationDate": "2021-01-04",
                        "applicationEndDate": "2021-03-09",
                        "status": "adimitted",
                        "conditions": null
                    },
                    {
                        "country": "uk",
                        "university": "university College London",
                        "department": "Electrical and Electronic Engineering",
                        "major": "Integrated Machine Learning Systems",
                        "degree": "MSc",
                        "referenceContribution": 6,
                        "applicationDate": "2021-11-21",
                        "applicationEndDate": "2021-02-14",
                        "status": "adimitted",
                        "conditions": null
                    }
                ],
                "decision": 0
            }
        },
        {
            "netid": "yimian.liu17",
            "nickname": "iotcat",
            "item": {
                "country": "uk",
                "university": "university College London",
                "department": "Electrical and Electronic Engineering",
                "major": "Integrated Machine Learning Systems",
                "degree": "MSc",
                "referenceContribution": 6,
                "applicationDate": "2021-11-21",
                "applicationEndDate": "2021-02-14",
                "status": "adimitted",
                "conditions": null
            },
            "meta": {
                "graduateYear": 2021,
                "department": "electrical & electronic engineering",
                "major": "electronic science techonology",
                "2plus2": true,
                "grade": {
                    "year2": 84,
                    "year0": 74,
                    "year1": 80,
                    "year3": null,
                    "gpa": 3.83,
                    "majorGpa": 3.99,
                    "rank": null,
                    "no1Grade": null,
                    "scholarship": "full"
                },
                "language": [],
                "tests": [],
                "internships": [
                    {
                        "title": "IETE欧朗物联",
                        "type": [
                            "iete",
                            "foreign"
                        ],
                        "length": 60,
                        "relavence": 10,
                        "gain": 9.6
                    }
                ],
                "projects": [
                    {
                        "title": "智慧农业",
                        "type": [
                            "surf",
                            "university"
                        ],
                        "length": 60,
                        "relavence": 10,
                        "gain": 6.8
                    },
                    {
                        "title": null,
                        "type": [
                            "diy"
                        ],
                        "length": 358,
                        "relavence": 9.2,
                        "gain": 8.6
                    }
                ],
                "papers": [],
                "competitions": [
                    {
                        "title": null,
                        "relavence": 6.7,
                        "contribution": 4.5,
                        "award": null,
                        "value": 3.2
                    }
                ],
                "clubs": [
                    {
                        "title": "infoco",
                        "relavence": 7.6,
                        "value": 6.4,
                        "contribution": 1
                    }
                ],
                "agent": {
                    "title": null,
                    "plan": null,
                    "overall": null,
                    "knowledge": null,
                    "cvSkill": null,
                    "responsibility": null,
                    "cost": null
                },
                "applications": [
                    {
                        "country": "us",
                        "university": "Cornell university",
                        "department": "Electrical and Computer Engineering",
                        "major": "Electrical and Computer Engineering",
                        "degree": "MEng",
                        "referenceContribution": 9,
                        "applicationDate": "2021-01-04",
                        "applicationEndDate": "2021-03-09",
                        "status": "adimitted",
                        "conditions": null
                    },
                    {
                        "country": "uk",
                        "university": "university College London",
                        "department": "Electrical and Electronic Engineering",
                        "major": "Integrated Machine Learning Systems",
                        "degree": "MSc",
                        "referenceContribution": 6,
                        "applicationDate": "2021-11-21",
                        "applicationEndDate": "2021-02-14",
                        "status": "adimitted",
                        "conditions": null
                    }
                ],
                "decision": 0
            }
        }
    ]
}
```




## setForm

推送一个form对象到服务器。

### 地址

```
POST /setForm
```

### 参数

> Method: `x-www-form-urlencoded`

 - `form`: [JSON格式form对象](/pages/dictionary?id=formobj)

### 返回值

[JSON格式status对象](/pages/dictionary?id=statusobj)

#### 示例

```json
{
    "status": true,
    "statusCode": 0,
    "message": "Successful!",
    "data": {
        "acknowledged": true,
        "modifiedCount": 1,
        "upsertedId": null,
        "upsertedCount": 0,
        "matchedCount": 1
    }
}
```

含义详见[sdk.set函数返回值](/pages/sdk?id=resolve)

## getForm

从服务器获取指定form对象。

### 地址

```
GET /getForm
```

### 参数

 - `netid`: 西浦id

### 返回值

[JSON格式status对象](/pages/dictionary?id=statusobj)

#### 示例

```json
{
    "status": true,
    "statusCode": 0,
    "message": "Successful!",
    "data": {
        "_id": "60f38d4411e7ca5ff3bf8e99",
        "userProfile": {
            "netid": "yimian.liu17",
            "domain": "student.xjtlu.edu.cn",
            "email": [
                "i@yimian.xyz"
            ],
            "nickname": "iotcat",
            "gender": "male"
        },
        "article": {
            "format": "markdown",
            "data": "肥肠肥肠长的经验分享文~~~"
        },
        "feedback": {
            "data": null
        },
        "meta": {
            "graduateYear": 2021,
            "department": "electrical & electronic engineering",
            "major": "electronic science techonology",
            "2plus2": true,
            "grade": {
                "year2": 84,
                "year0": 74,
                "year1": 80,
                "year3": null,
                "gpa": 3.83,
                "majorGpa": 3.99,
                "rank": null,
                "no1Grade": null,
                "scholarship": "full"
            },
            "language": [],
            "tests": [],
            "internships": [
                {
                    "title": "IETE欧朗物联",
                    "type": [
                        "iete",
                        "foreign"
                    ],
                    "length": 60,
                    "relavence": 10,
                    "gain": 9.6
                }
            ],
            "projects": [
                {
                    "title": "智慧农业",
                    "type": [
                        "surf",
                        "university"
                    ],
                    "length": 60,
                    "relavence": 10,
                    "gain": 6.8
                },
                {
                    "title": null,
                    "type": [
                        "diy"
                    ],
                    "length": 358,
                    "relavence": 9.2,
                    "gain": 8.6
                }
            ],
            "papers": [],
            "competitions": [
                {
                    "title": null,
                    "relavence": 6.7,
                    "contribution": 4.5,
                    "award": null,
                    "value": 3.2
                }
            ],
            "clubs": [
                {
                    "title": "infoco",
                    "relavence": 7.6,
                    "value": 6.4,
                    "contribution": 1
                }
            ],
            "agent": {
                "title": null,
                "plan": null,
                "overall": null,
                "knowledge": null,
                "cvSkill": null,
                "responsibility": null,
                "cost": null
            },
            "applications": [
                {
                    "country": "us",
                    "university": "Cornell university",
                    "department": "Electrical and Computer Engineering",
                    "major": "Electrical and Computer Engineering",
                    "degree": "MEng",
                    "referenceContribution": 9,
                    "applicationDate": "2021-01-04",
                    "applicationEndDate": "2021-03-09",
                    "status": "adimitted",
                    "conditions": null
                },
                {
                    "country": "uk",
                    "university": "university College London",
                    "department": "Electrical and Electronic Engineering",
                    "major": "Integrated Machine Learning Systems",
                    "degree": "MSc",
                    "referenceContribution": 6,
                    "applicationDate": "2021-11-21",
                    "applicationEndDate": "2021-02-14",
                    "status": "adimitted",
                    "conditions": null
                }
            ],
            "decision": 0
        },
        "userPreference": {
            "anonymous": false,
            "notify": true
        },
        "version": 0.1
    }
}
```


## reset

重置服务端数据(**仅供测试使用**)

### 地址

```
GET /reset
```

### 参数

无

### 返回值

[JSON格式status对象](/pages/dictionary?id=statusobj)

#### 示例

```json
{
    "status": true,
    "statusCode": 0,
    "message": "Successful!",
    "data": true
}
```