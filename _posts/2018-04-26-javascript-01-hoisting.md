---
layout: post
title: Hoisting 걔념
date: 2018-04-26 23:18:04 +0900
description: Javascript Hoisting 걔념 알아보기
img: javascript.png
tags: [javascript]
---
-------------------------------------
오늘은 자바 스크립트의 **Hoisting** 걔념에 대해서 알아보겠습니다.
**Hoisting**은 사실 매우 단순한 걔념이지만 모르고 그냥 지나치시는 분이 많은 듯 합니다.

**Hoisting** 을 간단하게 설명하자면 함수나 변수의 선언을 나중에 할 수 있다는 걔념입니다. 자바스크립트의 기본 걔념으로 스크립트가 실행 될 때
```javascript
test = 5; // 선언되기 전에 값이 assign되었습니다.

console.log(test); // 결과값으로 5가 출력됩니다.

var test; // 여기서 변수가 선언되었습니다.
```
함수도 마찬가지 입니다.
```javascript
console.log(addNums(5, 6)); // 선언되기전 함수가 사용 되었습니다.

function addNums(a, b) { // 사용된 후에 함수가 선언되었습니다.
  return a + b;
}
```

물론 함수나 변수가 사용 되는 위치보다 위에다 선언할 수도 있습니다. 오히려 많은 코딩 컨벤션들이 선언부는 파일의 상위단에 적는걸 권장하고 있습니다. [AirBnb Coding Convention 바로가기](https://github.com/airbnb/javascript#hoisting)

### 햇갈릴 수 있는 걔념
한가지 주의 할점은 **선언**은 나중에 올 수 있지만 **초기화**는 나중에 올 수 없다는 점 입니다. 아래의 예에서 차이를 비교해 보겠습니다.
```javascript
// 선언 Hoisting
var a = 5;
b = 3;

console.log(a + b); // 출력값은 8입니다.

var b;
```

```javascript
// 초기화(Hoising 사용의 잘못된 예)
var a = 5;

console.log(a + b); // 에러가 출력됩니다. b is undefined

var b = 3;
```

예에서 확인 할 수 있듯이 Hoising을 잘 못 이해할 경우 에러가 발생할 수 있습니다.
그렇다면 무조건 선언과 초기화를 같이 파일 상단에 위치 시키는 것이 좋은 걸까요? 앞에서도 언급했듯이 많은 코딩규약들이 권장하고 있지만 전 개인적으로 변수나 상수의 선언과 초기화는 **상단부**, 함수의 선언은 **하단부**에 선언하는 걸 선호합니다. 아래와 같은 구조가 되겠네요.

```javascript
const a = 'abc';
const b = 10;
const c = 'hello world';

$(document).ready(() => {
  // 여기서 선언된 함수들을 사용
});

// 하단부에 함수 선언
function addNums(b, d) {
  return b + d;
}
```

제가 평소 파일을 작성하는 구조와 비슷하게 적어보았습니다. 제가 사용하는 방법이 최선은 아니겠지만 이런 구조가 개인적으로 가독성이 올라가는 것 같습니다. 실제로 화면단과 연결되있는 이벤트들이 어떤 함수들을 이용하는지 보고 아래로 내려가서 그 함수가 어떻게 정의 되어 있나 확인하는 식이 되겠네요. 화면에서부터 거꾸로 타고 들어가는 구조입니다. 저처럼 이런 방식이 편한 사람이 있기때문에 Hoisting 걔념도 탄생된게 아닐까 합니다.

<br/>
### 함수 선언식과 표현식의 Hoisting 차이
함수의 Hoisting 걔념으로 한가지 예를 더 들어보겠습니다.

```javascript
console.log(addNums1(3, 4)) // 7
console.log(addNums2(3, 4)) // Uncaught TypeError: addNums2 is not a function

// 함수 선언식
function addNums1(b, d) {
  return b + d;
}

// 함수 표현식
var addNums2 = function (b, d) {
  return b + d;
}
```

동일한 구조의 함수이지만 선언 형식에 따라 Hoisting 결과에 차이가 납니다. 앞서 말씀 드렸듯이 Hoisting 은 **선언부에만 해당** 되고 초기값은 Hoisting되지 않습니다. 때문에 스코프를 포함한 선언 자체인 addNum1은 함수가 Hoisting되지만 addNums2의 경우는 함수를 담을 그릇인 addNums2의 선언 부부분만 Hoisting되었습니다.

위의 예가 Hoisting 된 모습은 아래와 같습니다.

```javascript
function addNums1(b, d) {
  return b + d;
}
var addNums2

console.log(addNums1(3, 4)) // 7
console.log(addNums2(3, 4)) // Uncaught TypeError: addNums2 is not a function

addNums2 = function (b, d) {
  return b + d;
}
```