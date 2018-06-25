---
layout: post
title: Javascript 걔념정리 - Copy Object
date: 2018-06-25 07:26:09 +0900
description: Javascript Object 복사하기
img: javascript.png
tags: [javascript]
---
------------------------------------------------
Javascript 를 접한지 얼마 되지 않은 초보 개발자들이 흔히 저지르는 실수가 객체를 복사할 경우에 빈번하게 발생합니다.<br/>
원인은 객체의 **복사** 와 **참조** 의 걔념을 분명히 이해하지 못했기 때문입니다. 아래에서 어떤 예가 있는지 살펴보겠습니다.

### 객체 참조의 예
```javascript
var obj1 = {name: "Dave"};
var obj2 = obj1;

console.log(obj2.name) // Dave

obj2.name = "Chris"; // obj2의 이름 변경

console.log(obj2.name) // Chris
console.log(obj1.name) // Chris
```

위의 예와 같이 분명히 **ojb2** 의 소속 프로퍼티를 변경하였는데 **obj1** 까지 같이 변경 되었습니다. 원인은 ` = ` (assign operator) 를 이용해서 객체를 복사할 경우 실제 객체가 아닌 실제 객체의 **주소값을 복사** 하게 되기 때문입니다. obj2 와 obj1 이 결국 같은 객체를 공유하고 있는 모양이기 때문에 한쪽을 변경하게 될 경우 다른쪽도 변경되게 됩니다.

그렇다면 이제 실제로 객체를 복사하는 방법을 알아보겠습니다. 객체 복사의 방법으로는 **Shallow Copy** 와 **Deep Copy** 로 크게 나눌 수 있습니다.

### 1.Shallow Copy

```javascript
var obj1 = {name: "Dave" ,hobby: {one: "swimming"}};
var obj2 = Object.create(obj1);
/* 아래의 카피방법들은 모두 동일한 결과로 복사됩니다. */
// var obj2 = Object.assign({}, obj1); // ES6 Shallow copy
// var obj2 = _.clone(obj1); // underscore 를 이용한 shallow copy
// var obj2 = $.extend({}, obj1); // jquery 를 이용한 shallow copy

console.log(obj2.name) // Dave

obj2.name = "Chris"; // obj2의 이름 변경
obj2.hobby.one = "baseball"; // obj2.hobby.one 변경

console.log(obj2.name) // Chris
console.log(obj1.name) // Dave
console.log(obj2.hobby.one) // baseball
console.log(obj1.hobby.one) // baseball
```

위와같이 **Object** 객체의 **create** 메소드를 이용해 obj1을 복사했습니다. 결과를 보면 알 수 있듯이 주소 값을 참조한 것이 아닌 실제 객체를 복사하였습니다. 하지만 여기서도 문제는 있습니다. 실제 객체는 복사하였지만 객체의 프로퍼티인 *hobby* 객체의 *one* 프로퍼티는 주소값이 참조 되었습니다. 이러한 복사를 **shallow Copy** (얕은 복사) 라고 합니다.

### 2.Deep Copy

Deep Copy는 이름에서도 예상할 수 있듯이 객체의 모든 하위계층 까지 실제로 복사되는 것을 의미합니다.

```javascript
var obj1 = {deep: {obj: "object1"}};
// 1. String으로 변환후 다시 Object화해서 복사
var obj2 = JSON.parse(JSON.stringify(obj1));
// 2. jquery의 extend 메소드는 첫번째 인자로 deep copy 인지 아닌지 판단합니다.
var obj3 = $.extend(true, {}, obj1);

obj2.deep.obj = "object2";
obj3.deep.obj = "object3";

console.log(obj1.deep.obj) // object1
console.log(obj2.deep.obj) // object2
console.log(obj3.deep.obj) // object3
```