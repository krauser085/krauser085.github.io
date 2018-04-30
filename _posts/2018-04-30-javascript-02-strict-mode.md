---
layout: post
title: Strict Mode 사용하기
date: 2018-04-30 14:30:53 +0900
description: Javascript의 Strict Mode 의 사용법 알아보기ㅣ
img: javascript.png
tags: [javascript]
---
-------------------------------------
### Strict Mode란?
**Strict Mode** ES5(ECMAScript version 5)부터 나온 걔념입니다. 간단하게 정의하자면 변수, 상수, 함수 등은 반드시 정의 되어야 한다는 걔념입니다. 간단하게 Strict Mode를 **적용 했을 때**와 **적용하지 않았을 때** 를 비교해 보겠습니다. 
- 적용하지 않았을 때
```javascript
num = 10;
console.log(num); // ==> 10이 출력됨
```
- 적용했을 때
```javascript
'use strict';
num = 10;
console.log(num); // num is not undefined error가 발생합니다.
```
적용했을 때 에러가 발생한 이유는 strict mode임에도 불구하고 변수가 선언되지 않았기 때문입니다. 아래와 같이 수정할 경우 에러는 발생하지 않습니다.
```javascript
'use strict';
var num = 10; // 선언과 동시에 초기화 하였습니다. 
console.log(num); // 10 이 정상적으로 출력됩니다.
```

물론 strict mode 에서도 [hoisting](/javascript-01-hoisting/)걔념은 적용되기 때문에 나중에 선언되어도 한 파일 안에 선언만 되어 있다면 사용할 수 있습니다.
```javascript
'use strict';
num = 10; // 선언하기전 값이 초기화 되었습니다.
console.log(num); // 10 이 정상적으로 출력됩니다.
var num; // 여기서 선언한 변수가 hoisting 됩니다.
```

한가지 더 알아두셔야 될 부분은 strict mode의 **적용범위** 를 설정할 수 있다는 점 입니다.
```javascript
num = 10; 
console.log(num); // 선언하지 않았지만 10이 정상적으로 출력됩니다.
withStrict();

function withStrict() {
  'use strict'; // 함수 안에 적용되었습니다.
  num2 = 7;
  console.log(num2); // num2 is undefined error가 발생합니다.
}
```

## 왜 **Strict Mode**를 사용해야 할까?
strict Mode를 사용하게 되면 불필요한 에러를 줄일 수 있습니다. 한가지 예를 들어보자면 num이란 변수를 사용해서 무언가 결과를 도출하려고 합니다. 하지만 개발자가 타이핑 실수로 num 이란 변수가 아닌 nom 이란 변수에 값을 대입했다 가정합니다. strict mode 를 사용하지 않으면 당연히 에러도 발생하지 않겠지요. 에러가 발생하지 않는데 원하는 결과 값이 도출 되지 않는 경우, 원인을 찾기가 상당히 힘들 수 있습니다. (프로젝트 규모의 따라서 노동량이 달라질 수 있겠지요.) 이런 작은 실수 들을 줄이기 위해서라도 Strict Mode를 사용하는 것은 좋은 습관이라고 할 수 있습니다. 대부분 Javascript를 사용해 개발하는 프로젝트의 경우 일단 파일 첫 머리에서 `'use strict';`를 선언해주고 시작하는 것이 일반적입니다.