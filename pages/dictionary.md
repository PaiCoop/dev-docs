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
		"email": s => s instanceof Array && s.every(i=>/^([A-Za-z0-9_\-\.\u4e00-\u9fa5])+\@([A-Za-z0-9_\-\.])+\.([A-Za-z]{2,8})$/.test(i)) ? s : null,
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
			"majorGpa": s => typeof s === 'number' && s >= 0 && s <= 4 ? s : null,
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
			"type": s => s instanceof Array && s.subsetTo(['surf', 'inclass', 'company', 'university', 'diy']) ? s : null,
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
			"plan": s => typeof s === 'string' && ['half', 'all'].includes(s) ? s : null,
			"overall": s => typeof s === 'number' && s >= 0 && s <= 10 ? s : null,
			"knowledge": s => typeof s === 'number' && s >= 0 && s <= 10 ? s : null,
			"cvSkill": s => typeof s === 'number' && s >= 0 && s <= 10 ? s : null,
			"responsibility": s => typeof s === 'number' && s >= 0 && s <= 10 ? s : null,
			"cost": s => typeof s === 'number' && s >= 0 && s <= 10 ? s : null
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


### FormObj生成器

> 点击下方按钮随机生成FormObj

<button onclick="
function Random(min, max) {
    return Math.round(Math.random() * (max - min)) + min;
}
function randomString(length) {
    var str = 'abcdefghijklmnopqrstuvwxyz';
    var result = '';
    for (var i = length; i > 0; --i) 
        result += str[Math.floor(Math.random() * str.length)];
    return result;
}
function randomEmail(){
	return '&quot;'+randomString(Random(5,13))+'@'+randomString(Random(2,8))+'.com'+'&quot;';
}
function randomLanguage(){
	let s = '<span class=&quot;token punctuation&quot;>{</span>';
    s += `
            <span class=&quot;token property&quot;>&quot;type&quot;</span><span class=&quot;token operator&quot;>:</span> &quot;${randomSelect(['ielts', 'toefl', 'duolingo', 'pte'])}&quot;<span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;grade&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token string&quot;>${randomSelect(['&quot;'+randomString(Random(5, 20))+'&quot;'])}</span>`;
    s += `
        <span class=&quot;token punctuation&quot;>}</span>`;
    return s;
}
function randomTest(){
	let s = '<span class=&quot;token punctuation&quot;>{</span>';
    s += `
            <span class=&quot;token property&quot;>&quot;type&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token string&quot;>${randomSelect(['&quot;'+randomString(Random(5, 30))+'&quot;'])}</span><span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;grade&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token string&quot;>${randomSelect(['&quot;'+randomString(Random(5, 20))+'&quot;'])}</span>`;
    s += `
        <span class=&quot;token punctuation&quot;>}</span>`;
    return s;
}
function randomInternship(){
	let s = '<span class=&quot;token punctuation&quot;>{</span>';
    s += `
            <span class=&quot;token property&quot;>&quot;title&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token string&quot;>${randomSelect(['&quot;'+randomString(Random(5, 30))+'&quot;', undefined])}</span><span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;type&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token punctuation&quot;>[</span>${concatArray(Random(1,2), ()=>randomSelect(['top500', 'iete', 'gov', 'foreign']), '<span class=&quot;token string&quot;>&quot;', '&quot;</span>', '<span class=&quot;token punctuation&quot;>, </span>')}<span class=&quot;token punctuation&quot;>]</span><span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;length&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token number&quot;>${Random(7, 300)}</span><span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;relavence&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token number&quot;>${Random(0, 10)}</span><span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;gain&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token number&quot;>${Random(0, 10)}</span>`
    s += `
        <span class=&quot;token punctuation&quot;>}</span>`;
    return s;
}
function randomProject(){
	let s = '<span class=&quot;token punctuation&quot;>{</span>';
    s += `
            <span class=&quot;token property&quot;>&quot;title&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token string&quot;>${randomSelect(['&quot;'+randomString(Random(5, 30))+'&quot;', undefined])}</span><span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;type&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token punctuation&quot;>[</span>${concatArray(Random(1,2), ()=>randomSelect(['surf', 'inclass', 'company', 'university', 'diy']), '<span class=&quot;token string&quot;>&quot;', '&quot;</span>', '<span class=&quot;token punctuation&quot;>, </span>')}<span class=&quot;token punctuation&quot;>]</span><span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;length&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token number&quot;>${Random(7, 300)}</span><span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;relavence&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token number&quot;>${Random(0, 10)}</span><span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;gain&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token number&quot;>${Random(0, 10)}</span>`
    s += `
        <span class=&quot;token punctuation&quot;>}</span>`;
    return s;
}
function randomPaper(){
	let s = '<span class=&quot;token punctuation&quot;>{</span>';
    s += `
            <span class=&quot;token property&quot;>&quot;title&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token string&quot;>${randomSelect(['&quot;'+randomString(Random(5, 30))+'&quot;', undefined])}</span><span class=&quot;token punctuation&quot;>,</span>`;
     s += `
            <span class=&quot;token property&quot;>&quot;level&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token number&quot;>${Random(0, 10)}</span><span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;authorType&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token punctuation&quot;>[</span>${concatArray(Random(1,2), ()=>randomSelect(['first', 'last', 'corresponding']), '<span class=&quot;token string&quot;>&quot;', '&quot;</span>', '<span class=&quot;token punctuation&quot;>, </span>')}<span class=&quot;token punctuation&quot;>]</span><span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;relavence&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token number&quot;>${Random(0, 10)}</span>`;
    s += `
        <span class=&quot;token punctuation&quot;>}</span>`;
    return s;
}
function randomCompet(){
	let s = '<span class=&quot;token punctuation&quot;>{</span>';
    s += `
            <span class=&quot;token property&quot;>&quot;title&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token string&quot;>${randomSelect(['&quot;'+randomString(Random(5, 30))+'&quot;', undefined])}</span><span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;contribution&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token number&quot;>${Random(0, 10)}</span><span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;value&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token number&quot;>${Random(0, 10)}</span><span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;relavence&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token number&quot;>${Random(0, 10)}</span><span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;award&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token string&quot;>${randomSelect(['&quot;'+randomString(Random(5, 50))+'&quot;', undefined])}</span>`;    
    s += `
        <span class=&quot;token punctuation&quot;>}</span>`;
    return s;
}
function randomClub(){
	let s = '<span class=&quot;token punctuation&quot;>{</span>';
    s += `
            <span class=&quot;token property&quot;>&quot;title&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token string&quot;>${randomSelect(['&quot;'+randomString(Random(5, 30))+'&quot;', undefined])}</span><span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;contribution&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token number&quot;>${Random(0, 10)}</span><span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;value&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token number&quot;>${Random(0, 10)}</span><span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;relavence&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token number&quot;>${Random(0, 10)}</span>`; 
    s += `
        <span class=&quot;token punctuation&quot;>}</span>`;
    return s;
}
function randomAgent(){
	let s = '<span class=&quot;token punctuation&quot;>{</span>';
    s += `
            <span class=&quot;token property&quot;>&quot;title&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token string&quot;>${randomSelect(['&quot;'+randomString(Random(5, 30))+'&quot;', undefined])}</span><span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;plan&quot;</span><span class=&quot;token operator&quot;>:</span> &quot;${randomSelect(['half', 'all', undefined])}&quot;<span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;overall&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token number&quot;>${Random(0, 10)}</span><span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;knowledge&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token number&quot;>${Random(0, 10)}</span><span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;cvSkill&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token number&quot;>${Random(0, 10)}</span><span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;responsibility&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token number&quot;>${Random(0, 10)}</span><span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;cost&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token number&quot;>${Random(0, 10)}</span>`; 
    s += `
        <span class=&quot;token punctuation&quot;>}</span>`;
    return s;
}
function randomApp(){
	let s = '<span class=&quot;token punctuation&quot;>{</span>';
    s += `
            <span class=&quot;token property&quot;>&quot;country&quot;</span><span class=&quot;token operator&quot;>:</span> &quot;${randomSelect(['cn', 'uk', 'us', 'canada', 'hk', 'ca', 'sg', 'eu', 'au', 'other'])}&quot;<span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;university&quot;</span><span class=&quot;token operator&quot;>:</span> &quot;${randomSelect(['Cornell University', 'University of Liverpool', 'Standford University', 'University College London', 'Imperial College London', 'Duke University', 'Harvard University', 'Beijing University', 'National University of Sigapore', 'New York University', 'University of Edinburgh', 'King College London', 'Hongkong University', 'Hongkong Chinese University', 'Tsinghua University', 'University of Cambridge', 'Columbia University', 'University of Oxford', 'Yale University', 'University of Chicago', 'Massachusetts Institute of Technology', 'University of California, Berkeley', 'Princeton University', 'Johns Hopkins University', 'University of Pennsylvania', 'University of Michigan', 'Carnegie Mellon University', 'University of Washington', 'University of California, San Diego', 'Georgia Institute of Technology', 'University of Illinois at Urbana Champaign'])}&quot;<span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;department&quot;</span><span class=&quot;token operator&quot;>:</span> &quot;${randomSelect(['Anthropology Department', 'Cardiothoracic Surgery Department', 'Classics Department', 'Computer Science Department', 'Neurobiology Department', 'Economics Department', 'Electrical Engineering Department'])}&quot;<span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;major&quot;</span><span class=&quot;token operator&quot;>:</span> &quot;${randomSelect(['Electrical and Computer Engineering', 'Computer Science', 'Biomedical Engineering', 'Mathematics', 'Mechanical Engineering', 'Applied Physics', 'Atmospheric Science', 'Civil and Environmental Engineering', 'Geological Science', 'Chemical Engineering', 'Physics', 'Materials Science and Engineering'])}&quot;<span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;degree&quot;</span><span class=&quot;token operator&quot;>:</span> &quot;${randomSelect(['MSc', 'MEng', 'MPhil', 'PhD', 'BEng', 'BSc', 'other'])}&quot;<span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;applicationDate&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token string&quot;>${randomSelect(['&quot;'+Random(2019, 2021)+'-'+Random(1, 12)+'-'+Random(1, 28)+'&quot;'])}</span><span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;applicationEndDate&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token string&quot;>${randomSelect(['&quot;'+Random(2019, 2021)+'-'+Random(1, 12)+'-'+Random(1, 28)+'&quot;'])}</span><span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;status&quot;</span><span class=&quot;token operator&quot;>:</span> &quot;${randomSelect(['adimitted', 'rejected', 'waitlist', 'onhold'])}&quot;<span class=&quot;token punctuation&quot;>,</span>`;
    s += `
            <span class=&quot;token property&quot;>&quot;conditions&quot;</span><span class=&quot;token operator&quot;>:</span> <span class=&quot;token string&quot;>${randomSelect(['&quot;'+randomString(Random(5, 50))+'&quot;', undefined])}</span>`;   
    s += `
        <span class=&quot;token punctuation&quot;>}</span>`;
    return s;
}
function concatArray(num, func, pre, post, spr){
	let s = '';
	for(let i = 0; i < num; i ++){
		if(i) s += spr || ', ';
		s += (pre?pre:'')+func()+(post?post:'');
	}
	return s;
}
function randomSelect(arr){
	return arr[Random(0, arr.length-1)]
}
(function () {
	function set(id, body, notStr){
		document.getElementById(id).innerHTML = (notStr||body===undefined||body===null||body===true||body===false?'':'&quot;')+body+(notStr||body==undefined||body===null||body===true||body===false?'':'&quot;');
	};
	set('netid', randomString(Random(4,12))+'.'+randomString(Random(2,6))+ Random(6,21));
	set('email', concatArray(Random(0, 3), randomEmail), true);
	set('nickname', randomSelect([randomString(Random(4, 21)), undefined]));
	set('domain', randomSelect(['student.xjtlu.edu.cn', 'xjtlu.edu.cn', 'alumni.xjtlu.edu.cn']));
	set('gender', randomSelect(['male', 'female', 'other']));
	set('anonymous', randomSelect([true, false]));
	set('notify', randomSelect([true, false]));
	set('graduateYear', Random(2010, 2021), true);
	set('department', randomSelect(['Electrical & Electronic Engineering', 'Mathematics', 'Computer Science']));
	set('major', randomSelect(['Electronic Science Techonology', 'Electrical Engineering']));
	set('2plus2', randomSelect([true, false]));
	set('year2', Random(40, 99), true);
	set('year1', randomSelect([Random(40,88), undefined]), true);
	set('year0', randomSelect([Random(30, 80), undefined]), true);
	set('gpa', randomSelect([Random(200, 400)/100, undefined]), true);
	set('majorGpa', randomSelect([Random(300, 400)/100, undefined]), true);
	set('rank', randomSelect([Math.random().toFixed(2), undefined]), true);
	set('no1Grade', randomSelect([Random(80, 100), undefined]), true);
	set('scholarship', randomSelect(['full', 'half', undefined]));
	set('languages', concatArray(Random(0, 3), randomLanguage, null, null, '<span class=&quot;token punctuation&quot;>, </span>'), true);
	set('tests', concatArray(Random(0, 3), randomTest, null, null, '<span class=&quot;token punctuation&quot;>, </span>'), true);
	set('internships', concatArray(Random(0, 3), randomInternship, null, null, '<span class=&quot;token punctuation&quot;>, </span>'), true);
	set('projects', concatArray(Random(0, 3), randomProject, null, null, '<span class=&quot;token punctuation&quot;>, </span>'), true);
	set('papers', concatArray(Random(0, 2), randomPaper, null, null, '<span class=&quot;token punctuation&quot;>, </span>'), true);
	set('competitions', concatArray(Random(0, 3), randomCompet, null, null, '<span class=&quot;token punctuation&quot;>, </span>'), true);
	set('clubs', concatArray(Random(0, 3), randomClub, null, null, '<span class=&quot;token punctuation&quot;>, </span>'), true);
	set('agent', randomAgent(), true);
	set('apps', concatArray(Random(1, 6), randomApp, null, null, '<span class=&quot;token punctuation&quot;>, </span>'), true);
	set('article', randomSelect([randomString(Random(0, 10000)), undefined]));
})();
">Generate</button>


<pre v-pre="" data-lang="json" class="language-json"><code class="lang-json language-json" id="gForm"><span class="token punctuation">{</span>
    <span class="token property">"version"</span><span class="token operator">:</span> <span class="token number">0.1</span><span class="token punctuation">,</span>
    <span class="token property">"userProfile"</span><span class="token operator">:</span> <span class="token punctuation">{</span>
        <span class="token property">"netid"</span><span class="token operator">:</span> <span class="token string" id="netid">"yimian.liu17"</span><span class="token punctuation">,</span>
        <span class="token property">"domain"</span><span class="token operator">:</span> <span class="token string" id="domain">"student.xjtlu.edu.cn"</span><span class="token punctuation">,</span>
        <span class="token property">"email"</span><span class="token operator">:</span> <span class="token punctuation">[</span><span class="token string" id="email">"i@yimian.xyz"</span><span class="token punctuation">]</span><span class="token punctuation">,</span>
        <span class="token property">"nickname"</span><span class="token operator">:</span> <span class="token string" id="nickname">"iotcat"</span><span class="token punctuation">,</span>
        <span class="token property">"gender"</span><span class="token operator">:</span> <span class="token string" id="gender">"male"</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    <span class="token property">"userPreference"</span><span class="token operator">:</span> <span class="token punctuation">{</span>
        <span class="token property">"anonymous"</span><span class="token operator">:</span> <span class="token boolean" id="anonymous">false</span><span class="token punctuation">,</span>
        <span class="token property">"notify"</span><span class="token operator">:</span> <span class="token boolean" id="notify">true</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    <span class="token property">"meta"</span><span class="token operator">:</span> <span class="token punctuation">{</span>
        <span class="token property">"graduateYear"</span><span class="token operator">:</span> <span class="token number" id="graduateYear">2021</span><span class="token punctuation">,</span>
        <span class="token property">"department"</span><span class="token operator">:</span> <span class="token string" id="department">"Electrical &amp; Electronic Engineering"</span><span class="token punctuation">,</span>
        <span class="token property">"major"</span><span class="token operator">:</span> <span class="token string" id="major">"Electronic Science Techonology"</span><span class="token punctuation">,</span>
        <span class="token property">"2plus2"</span><span class="token operator">:</span> <span class="token boolean" id="2plus2">true</span><span class="token punctuation">,</span>
        <span class="token property">"grade"</span><span class="token operator">:</span> <span class="token punctuation">{</span>
            <span class="token property">"year2"</span><span class="token operator">:</span> <span class="token number" id="year2">84</span><span class="token punctuation">,</span>
            <span class="token property">"year1"</span><span class="token operator">:</span> <span class="token number" id="year1">80</span><span class="token punctuation">,</span>
            <span class="token property">"year0"</span><span class="token operator">:</span> <span class="token number" id="year0">74</span><span class="token punctuation">,</span>
            <span class="token property">"gpa"</span><span class="token operator">:</span> <span class="token number" id="gpa">3.83</span><span class="token punctuation">,</span>
            <span class="token property">"majorGpa"</span><span class="token operator">:</span> <span class="token number" id="majorGpa">3.99</span><span class="token punctuation">,</span>
            <span class="token property">"rank"</span><span class="token operator">:</span> <span class="token number" id="rank">undefined</span><span class="token punctuation">,</span>
            <span class="token property">"no1Grade"</span><span class="token operator">:</span> <span class="token number" id="no1Grade">undefined</span><span class="token punctuation">,</span>
            <span class="token property">"scholarship"</span><span class="token operator">:</span> <span class="token string" id="scholarship">"full"</span>
        <span class="token punctuation">}</span><span class="token punctuation">,</span>
        <span class="token property">"language"</span><span class="token operator">:</span> <span class="token punctuation">[</span><span id="languages"></span><span class="token punctuation">]</span><span class="token punctuation">,</span>
        <span class="token property">"tests"</span><span class="token operator">:</span> <span class="token punctuation">[</span><span id="tests"></span><span class="token punctuation">]</span><span class="token punctuation">,</span>
        <span class="token property">"internships"</span><span class="token operator">:</span> <span class="token punctuation">[</span><span id="internships"><span class="token punctuation">{</span>
            <span class="token property">"title"</span><span class="token operator">:</span> <span class="token string">"IETE欧朗物联"</span><span class="token punctuation">,</span>
            <span class="token property">"type"</span><span class="token operator">:</span> <span class="token punctuation">[</span><span class="token string">"iete"</span><span class="token punctuation">,</span> <span class="token string">"foreign"</span><span class="token punctuation">]</span><span class="token punctuation">,</span>
            <span class="token property">"length"</span><span class="token operator">:</span> <span class="token number">60</span><span class="token punctuation">,</span>
            <span class="token property">"relavence"</span><span class="token operator">:</span> <span class="token number">10</span><span class="token punctuation">,</span>
            <span class="token property">"gain"</span><span class="token operator">:</span> <span class="token number">9.6</span>
        <span class="token punctuation">}</span></span><span class="token punctuation">]</span><span class="token punctuation">,</span>
        <span class="token property">"projects"</span><span class="token operator">:</span> <span class="token punctuation">[</span><span id="projects"><span class="token punctuation">{</span>
            <span class="token property">"title"</span><span class="token operator">:</span> <span class="token string">"智慧农业"</span><span class="token punctuation">,</span>
            <span class="token property">"type"</span><span class="token operator">:</span> <span class="token punctuation">[</span><span class="token string">"surf"</span><span class="token punctuation">,</span> <span class="token string">"university"</span><span class="token punctuation">]</span><span class="token punctuation">,</span>
            <span class="token property">"length"</span><span class="token operator">:</span> <span class="token number">60</span><span class="token punctuation">,</span>
            <span class="token property">"relavence"</span><span class="token operator">:</span> <span class="token number">10</span><span class="token punctuation">,</span>
            <span class="token property">"gain"</span><span class="token operator">:</span> <span class="token number">6.8</span>
        <span class="token punctuation">}</span><span class="token punctuation">,</span> <span class="token punctuation">{</span>
            <span class="token property">"type"</span><span class="token operator">:</span> <span class="token punctuation">[</span><span class="token string">"diy"</span><span class="token punctuation">]</span><span class="token punctuation">,</span>
            <span class="token property">"length"</span><span class="token operator">:</span> <span class="token number">358</span><span class="token punctuation">,</span>
            <span class="token property">"relavence"</span><span class="token operator">:</span> <span class="token number">9.2</span><span class="token punctuation">,</span>
            <span class="token property">"gain"</span><span class="token operator">:</span> <span class="token number">8.6</span>
        <span class="token punctuation">}</span></span><span class="token punctuation">]</span><span class="token punctuation">,</span>
        <span class="token property">"papers"</span><span class="token operator">:</span> <span class="token punctuation">[</span><span id="papers"></span><span class="token punctuation">]</span><span class="token punctuation">,</span>
        <span class="token property">"competitions"</span><span class="token operator">:</span> <span class="token punctuation">[</span><span id="competitions"><span class="token punctuation">{</span>
            <span class="token property">"relavence"</span><span class="token operator">:</span> <span class="token number">6.7</span><span class="token punctuation">,</span>
            <span class="token property">"contribution"</span><span class="token operator">:</span> <span class="token number">4.5</span><span class="token punctuation">,</span>
            <span class="token property">"value"</span><span class="token operator">:</span> <span class="token number">3.2</span>
        <span class="token punctuation">}</span></span><span class="token punctuation">]</span><span class="token punctuation">,</span>
        <span class="token property">"clubs"</span><span class="token operator">:</span> <span class="token punctuation">[</span><span id="clubs"><span class="token punctuation">{</span>
            <span class="token property">"title"</span><span class="token operator">:</span> <span class="token string">"infoco"</span><span class="token punctuation">,</span>
            <span class="token property">"relavence"</span><span class="token operator">:</span> <span class="token number">7.6</span><span class="token punctuation">,</span>
            <span class="token property">"value"</span><span class="token operator">:</span> <span class="token number">6.4</span><span class="token punctuation">,</span>
            <span class="token property">"contribution"</span><span class="token operator">:</span> <span class="token number">1</span>
        <span class="token punctuation">}</span></span><span class="token punctuation">]</span><span class="token punctuation">,</span>
        <span class="token property">"agent"</span><span class="token operator">:</span><span id="agent"><span class="token punctuation">{</span><span class="token punctuation">}</span></span><span class="token punctuation">,</span>
        <span class="token property">"applications"</span><span class="token operator">:</span> <span class="token punctuation">[</span><span id="apps"><span class="token punctuation">{</span>
            <span class="token property">"country"</span><span class="token operator">:</span> <span class="token string">"us"</span><span class="token punctuation">,</span>
            <span class="token property">"university"</span><span class="token operator">:</span> <span class="token string">"Cornell university"</span><span class="token punctuation">,</span>
            <span class="token property">"department"</span><span class="token operator">:</span> <span class="token string">"Electrical and Computer Engineering"</span><span class="token punctuation">,</span>
            <span class="token property">"major"</span><span class="token operator">:</span> <span class="token string">"Electrical and Computer Engineering"</span><span class="token punctuation">,</span>
            <span class="token property">"degree"</span><span class="token operator">:</span> <span class="token string">"MEng"</span><span class="token punctuation">,</span>
            <span class="token property">"referenceContribution"</span><span class="token operator">:</span> <span class="token number">9</span><span class="token punctuation">,</span>
            <span class="token property">"applicationDate"</span><span class="token operator">:</span> <span class="token string">"2021-01-04"</span><span class="token punctuation">,</span>
            <span class="token property">"applicationEndDate"</span><span class="token operator">:</span> <span class="token string">"2021-03-09"</span><span class="token punctuation">,</span>
            <span class="token property">"status"</span><span class="token operator">:</span> <span class="token string">"adimitted"</span>
        <span class="token punctuation">}</span><span class="token punctuation">,</span> <span class="token punctuation">{</span>
            <span class="token property">"country"</span><span class="token operator">:</span> <span class="token string">"uk"</span><span class="token punctuation">,</span>
            <span class="token property">"university"</span><span class="token operator">:</span> <span class="token string">"university College London"</span><span class="token punctuation">,</span>
            <span class="token property">"department"</span><span class="token operator">:</span> <span class="token string">"Electrical and Electronic Engineering"</span><span class="token punctuation">,</span>
            <span class="token property">"major"</span><span class="token operator">:</span> <span class="token string">"Integrated Machine Learning Systems"</span><span class="token punctuation">,</span>
            <span class="token property">"degree"</span><span class="token operator">:</span> <span class="token string">"MSc"</span><span class="token punctuation">,</span>
            <span class="token property">"referenceContribution"</span><span class="token operator">:</span> <span class="token number">6</span><span class="token punctuation">,</span>
            <span class="token property">"applicationDate"</span><span class="token operator">:</span> <span class="token string">"2021-11-21"</span><span class="token punctuation">,</span>
            <span class="token property">"applicationEndDate"</span><span class="token operator">:</span> <span class="token string">"2021-02-14"</span><span class="token punctuation">,</span>
            <span class="token property">"status"</span><span class="token operator">:</span> <span class="token string">"adimitted"</span>
        <span class="token punctuation">}</span><span class="token punctuation">,</span> <span class="token punctuation">{</span>
            <span class="token property">"country"</span><span class="token operator">:</span> <span class="token string">"us"</span><span class="token punctuation">,</span>
            <span class="token property">"university"</span><span class="token operator">:</span> <span class="token string">"Duke University"</span><span class="token punctuation">,</span>
            <span class="token property">"department"</span><span class="token operator">:</span> <span class="token string">"Electrical and Computer Engineering"</span><span class="token punctuation">,</span>
            <span class="token property">"major"</span><span class="token operator">:</span> <span class="token string">"Electrical and Computer Engineering"</span><span class="token punctuation">,</span>
            <span class="token property">"degree"</span><span class="token operator">:</span> <span class="token string">"MSc"</span><span class="token punctuation">,</span>
            <span class="token property">"referenceContribution"</span><span class="token operator">:</span> <span class="token number">4</span><span class="token punctuation">,</span>
            <span class="token property">"applicationDate"</span><span class="token operator">:</span> <span class="token string">"2021-01-14"</span><span class="token punctuation">,</span>
            <span class="token property">"applicationEndDate"</span><span class="token operator">:</span> <span class="token string">"2021-02-03"</span><span class="token punctuation">,</span>
            <span class="token property">"status"</span><span class="token operator">:</span> <span class="token string">"adimitted"</span>
        <span class="token punctuation">}</span><span class="token punctuation">,</span> <span class="token punctuation">{</span>
            <span class="token property">"country"</span><span class="token operator">:</span> <span class="token string">"uk"</span><span class="token punctuation">,</span>
            <span class="token property">"university"</span><span class="token operator">:</span> <span class="token string">"University of Edinburgh"</span><span class="token punctuation">,</span>
            <span class="token property">"department"</span><span class="token operator">:</span> <span class="token string">"Informatics"</span><span class="token punctuation">,</span>
            <span class="token property">"major"</span><span class="token operator">:</span> <span class="token string">"Computer Science"</span><span class="token punctuation">,</span>
            <span class="token property">"degree"</span><span class="token operator">:</span> <span class="token string">"MSc"</span><span class="token punctuation">,</span>
            <span class="token property">"referenceContribution"</span><span class="token operator">:</span> <span class="token number">9</span><span class="token punctuation">,</span>
            <span class="token property">"applicationDate"</span><span class="token operator">:</span> <span class="token string">"2021-11-29"</span><span class="token punctuation">,</span>
            <span class="token property">"applicationEndDate"</span><span class="token operator">:</span> <span class="token string">"2021-05-02"</span><span class="token punctuation">,</span>
            <span class="token property">"status"</span><span class="token operator">:</span> <span class="token string">"adimitted"</span>
        <span class="token punctuation">}</span><span class="token punctuation">,</span> <span class="token punctuation">{</span>
            <span class="token property">"country"</span><span class="token operator">:</span> <span class="token string">"uk"</span><span class="token punctuation">,</span>
            <span class="token property">"university"</span><span class="token operator">:</span> <span class="token string">"University of Edinburgh"</span><span class="token punctuation">,</span>
            <span class="token property">"department"</span><span class="token operator">:</span> <span class="token string">"Informatics"</span><span class="token punctuation">,</span>
            <span class="token property">"major"</span><span class="token operator">:</span> <span class="token string">"Informatics"</span><span class="token punctuation">,</span>
            <span class="token property">"degree"</span><span class="token operator">:</span> <span class="token string">"MSc"</span><span class="token punctuation">,</span>
            <span class="token property">"referenceContribution"</span><span class="token operator">:</span> <span class="token number">9</span><span class="token punctuation">,</span>
            <span class="token property">"applicationDate"</span><span class="token operator">:</span> <span class="token string">"2021-12-03"</span><span class="token punctuation">,</span>
            <span class="token property">"applicationEndDate"</span><span class="token operator">:</span> <span class="token string">"2021-05-18"</span><span class="token punctuation">,</span>
            <span class="token property">"status"</span><span class="token operator">:</span> <span class="token string">"adimitted"</span>
        <span class="token punctuation">}</span></span><span class="token punctuation">]</span><span class="token punctuation">,</span>
        <span class="token property">"decision"</span><span class="token operator">:</span> <span class="token number">0</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    <span class="token property">"article"</span><span class="token operator">:</span> <span class="token punctuation">{</span>
        <span class="token property">"format"</span><span class="token operator">:</span> <span class="token string">"markdown"</span><span class="token punctuation">,</span>
        <span class="token property">"data"</span><span class="token operator">:</span> <span class="token string" id="article">"肥肠肥肠长的经验分享文~~~"</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    <span class="token property">"feedback"</span><span class="token operator">:</span> <span class="token punctuation">{</span><span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code><button class="docsify-copy-code-button"><span class="label">Copy to clipboard</span><span class="error">Error</span><span class="success">Copied</span></button></pre>



## ListObject

```js

/* Map */
FormArr => {
	let o = [];
	FormArr.forEach(user => o.push(...user.meta.applications.map(item => ({
		netid: user.userProfile.netid,
		nickname: user.userPreference.anonymous ? 'Anonymous' : (user.userProfile.nickname || user.userProfile.netid.replace(/\b(\w)(\w*)/g, ($0,$1,$2)=>$1.toUpperCase()+$2.toLowerCase())),
		item: item,
		meta: user.meta
	}))));
	return o;
}
```
