# 概述

字典规范定义了组件之间传递的数据包结构。


# 规范语法说明

返回值为`undefined`时，说明非法。


# 规范设计

## FormObject

```js
/* Additional Methods */
if(!Array.prototype.subsetTo){
	Array.prototype.subsetTo=function(arr){
		return this.every(v=>arr.includes(v))
	}
}

/* Mask */
{
	"version": s => s === 0.1 ? s : undefined,
	"userProfile": {
		"netid": s => s.includes('.') ? s.toLowerCase() : undefined,
		"domain": s => typeof s === 'string' && ['xjtlu.edu.cn', 'student.xjtlu.edu.cn', 'alumni.xjtlu.edu.cn'].includes(s.toLowerCase()) ? s.toLowerCase() : undefined, 
		"email": s => s instanceof Array && s.every(i=>/^([A-Za-z0-9_\-\.\u4e00-\u9fa5])+\@([A-Za-z0-9_\-\.])+\.([A-Za-z]{2,8})$/.test(i)) ? s : undefined,
		"nickname": s => typeof s === 'string' ? s : null,
		"gender": s => ['male', 'female', 'other'].includes(s) ? s : undefined
	},
	"userPreference": {
		"anonymous": s => typeof s === 'boolean' ? s : undefined,
		"notify": s => typeof s === 'boolean' ? s : undefined,
	},
	"meta": {
		"graduateYear": s => typeof s === 'number' && s >= 2010 && s <= new Date().getFullYear()+4 ? parseInt(s) : undefined,
		"department": s => typeof s === 'string' && s.length >= 2 ?s.toLowerCase() : undefined,
		"major": s => typeof s === 'string' && s.length >= 2 ? s.toLowerCase() : undefined,
		"2plus2": s => typeof s ==='boolean' ? s : undefined,
		"grade": {
			"year2": s => typeof s === 'number' && s >= 0 && s <= 100 ? s : undefined,
			"year0": s => typeof s === 'number' && s >= 0 && s <= 100 ? s : null,
			"year1": s => typeof s === 'number' && s >= 0 && s <= 100 ? s : null,
			"year3": s => typeof s === 'number' && s >= 0 && s <= 100 ? s : null,
			"gpa": s => typeof s === 'number' && s >= 0 && s <= 4 ? s : null,
			"majorGpa": s => typeof s === 'number' && s >= 0 && s <= 100 ? s : null,
			"rank": s => typeof s === 'number' && s >= 0 && s <= 1 ? s : null,
			"no1Grade": s => typeof s === 'number' && s >= 0 && s <= 100 ? s : null,
			"scholarship": s => typeof s === 'string' ? s : null
		},
		"language": [{
			"type": s => typeof s === 'string' && ['ielts', 'toefl', 'duolingo', 'pte'].includes(s) ? s : undefined,
			"grade": s => typeof s === 'string' ? s : undefined
		}],
		"tests": [{
			"type": s => typeof s === 'string' && s.length >= 2 ? s.toLowerCase() : undefined,
			"grade": s => typeof s === 'string' ? s.toLowerCase() : undefined
		}],
		"internships": [{
			"title": s => typeof s === 'string' ? s : null,
			"type": s => s instanceof Array && s.subsetTo(['top500', 'iete', 'gov', 'foreign']) ? s : null,
			"length": s => typeof s === 'number' && s >= 0 && s <= 1800 ? s : undefined,
			"relavence": s => typeof s === 'number' && s >= 0 && s <= 10 ? s : undefined,
			"gain": s => typeof s === 'number' && s >= 0 && s <= 10 ? s : undefined
		}],
		"projects": [{
			"title": s => typeof s === 'string' ? s : null,
			"type": s => s instanceof Array && s.subsetTo(['surf', 'inclass', 'company', 'university']) ? s : null,
			"length": s => typeof s === 'number' && s >= 0 && s <= 1800 ? s : undefined,
			"relavence": s => typeof s === 'number' && s >= 0 && s <= 10 ? s : undefined,
			"gain": s => typeof s === 'number' && s >= 0 && s <= 10 ? s : undefined
		}],
		"papers": [{
			"title": s => typeof s === 'string' ? s : null,
			"level": s => typeof s === 'number' && s >= 0 && s <= 10 ? s : undefined,
			"authorType": s => s instanceof Array && s.subsetTo(['first', 'last', 'corresponding']) ? s : null,
			"relavence": s => typeof s === 'number' && s >= 0 && s <= 10 ? s : undefined
		}],
		"competitions": [{
			"title": s => typeof s === 'string' ? s : null,
			"relavence": s => typeof s === 'number' && s >= 0 && s <= 10 ? s : undefined,
			"contribution": s => typeof s === 'number' && s >= 0 && s <= 10 ? s : undefined,
			"award": s => typeof s === 'string' ? s : null,
			"value": s => typeof s === 'number' && s >= 0 && s <= 10 ? s : undefined
		}],
		"clubs": [{
			"title": s => typeof s === 'string' ? s : null,
			"relavence": s => typeof s === 'number' && s >= 0 && s <= 10 ? s : undefined,
			"value": s => typeof s === 'number' && s >= 0 && s <= 10 ? s : undefined,
			"contribution": s => typeof s === 'number' && s >= 0 && s <= 10 ? s : undefined
		}],
		"agent": {
			"title": s => typeof s === 'string' ? s : null,
			"plan": s => typeof s === 'string' && ['half', 'all'].includes(s) ? s : undefined,
			"overall": s => typeof s === 'number' && s >= 0 && s <= 10 ? s : undefined,
			"knowledge": s => typeof s === 'number' && s >= 0 && s <= 10 ? s : undefined,
			"cvSkill": s => typeof s === 'number' && s >= 0 && s <= 10 ? s : undefined,
			"responsibility": s => typeof s === 'number' && s >= 0 && s <= 10 ? s : undefined,
			"cost": s => typeof s === 'number' && s >= 0 && s <= 10 ? s : undefined
		},
		"applications": [{
			"country": s => typeof s === 'string' && ['cn', 'uk', 'us', 'canada', 'hk', 'ca', 'sg', 'eu', 'au', 'other'].includes(s) ? s : undefined,
			"university": s => typeof s === 'string' ? s : undefined,
			"department": s => typeof s === 'string' ? s : undefined,
			"major": s => typeof s === 'string' ? s : undefined,
			"degree": s => typeof s === 'string' && ['MSc', 'MEng', 'MPhil', 'PhD', 'BEng', 'BSc', 'other'].includes(s) ? s : undefined,
			"referenceContribution": s => typeof s === 'number' && s >= 0 && s <= 10 ? s : null,
			"applicationDate": s => isNaN(s) && !isNaN(Date.parse(s)) ? s : undefined,
			"applicationEndDate":  s => isNaN(s) && !isNaN(Date.parse(s)) ? s : undefined,
			"status": s => typeof s === 'string' && ['adimitted', 'rejected', 'waitlist', 'onhold'].includes(s) ? s : undefined,
			"conditions": s => typeof s === 'string' ? s : null
		}],
		"decision": s => typeof s === 'number' && s >= 0 ? s : null
	},
	"article": {
		"format": s => typeof s === 'string' && ['markdown', 'html'].includes(s) ? s : undefined,
		"data": s => typeof s === 'string' ? s : null
	},
	"feedback": {
		"data": s => typeof s === 'string' ? s : null
	}
}
```



## ListObject

```js

/* Map */
FormArr => {
	let o = [];
	FormArr.forEach(user => o.push(...user.meta.applications.map(item => ({
		netid: user.userProfile.netid,
		item: item,
		meta: user.meta
	}))));
	return o;
}
```
