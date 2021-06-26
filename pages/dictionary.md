# 概述

字典规范定义了组件之间传递的数据包结构。


# 规范设计

## FormObject

```json
{
	"UserProfile": {
		"netid": "yimian.liu17",
		"email": [],
		"nickname": "",
		"gender": ""
	},
	"UserPreference": {
		"anonymous": false,
		"notify": true
	},
	"data": {
		"meta": {
			"department": "",
			"major": "",
			"2plus2": true,
			"grade": {
				"year0": null,
				"year1": null,
				"year2": null,
				"year3": null,
				"overall": 78
			},
			"researches": [{
				"title": "",
				"type": "surf|...",
				"description": "",
				"relavence": 0.89,
				"contribute": 0.67
			}, {}],
			"internships": [{
				"title": "",
				"type": "500|iete|...",
				"description": "",
				"relavence": 0.89,
				"contribution": 0.67
			}, {}],
			"agent": {
				"name": "",
				"plan": "",
				"contribution": 0.67
			},
			"applications": [{
				"university": "",
				"department": "",
				"major": "",
				"degree": "",
				"applicationDate": "date",
				"applicationEndDate": "date",
				"status": "rejected|admitted|waittinglist|waitting",
				"difficulty": 0.95,
				"reference": 0.54
			}, {}],
			"decision": 1, //applications_array_index
		},
		"article": {
			"format": "markdown",
			"data": ""
		},
		"feedback": {
			"data": ""
		}
	}
}
```
