---
layout: post
title: Javascript - doller sign ($), underscor sign (_)
date: 2018-08-13 23:25:42 +0900
description: Javascript에서 관습적으로 사용되는 $, _ 에 대해 알아보기
img: javascript.png
tags: [javascript]
---
------------------------------------------------

자바 스크립트에서 달러마크 ( **$** ) 와 언더스코어 ( **_** ) 는 다른 특수문자 들과 달리 알파벳들 처럼 하나의 문자로 취급됩니다. 때문에 언어 스펙상에서는 아무런 기능은 없지만 자바스크립트 프로그래머들은 보편적으로 의미를 부여해 사용해왔습니다.

<br/>
## Dollor Sign **$**
**document.getElementById()** 나 **document.querySelector()** 와 같은 함수들은 자바스크립트에서 가장 광범위하게 사용되는 함수들이 아닐까 합니다. 달러사인은 이렇게 빈번하게 사용되는 함수의 약자로 쓰여왔습니다.
때문에 Jquery와 같은 라이브러리들도 동일하게 DOM 쿼리시 $() 와 같이 달러마크를 사용하고 있습니다.
Jquery같은 라이브러리를 사용하지 않더라도 아래와 같이 정의해주면 동일하게 사용할 수 있습니다. 이렇게 사용하는 개발자들이 많았기 때문에 Jquery 같은 라이브러리에서도 채택했겠지요?
```javascript
function $(x) { return document.querySelectorAll(x); }
```
달러마크는 단독적으로 함수나 변수명으로 사용되는 경우가 없기 때문에 가장 프로그래머들이 사용하기 편했던것 같습니다.

<br/>
## Underscore **_**
언더스코어 역시 언어스펙상에서의 아무런 제약이 없는 개발문화상의 이야기 입니다.
언더스코어는 객체안의 private 프로퍼티를 나타내기 위해 흔히 사용됩니다.
설명해 주지 않아도 누구나 알고 있는 개발자들만의 은어라고 볼 수 있을 것 같습니다.

참조글 출처 : https://www.thoughtco.com/and-in-javascript-2037515