---
layout: post
title: Javascript 걔념정리 - this
date: 2018-07-02 13:45:27 +0900
description: Javascript에서의 this의 이해
img: javascript.png
tags: [javascript]
---
------------------------------------------------
### this 란
Javascript 로 만들어지는 모든 프로그램은 각각의 **객체** 로 구성되어 있습니다. 그리고 이 객체가 자기 스스로를 지칭하는 구문을 **this** 라고 합니다.

### 기본적인 사용법
```javascript
var obj = {
  hello: 'hello world!',
  print: function() {
    console.log(this.hello);
  }
}
obj.print(); // hello world!
```

위의 예에서 볼 수 있듯이 obj 란 객체를 선언했습니다. obj 객체 안에 메소드를 추가했고 그 메소드 안에서 this를 부를 경우 이 **this는 obj객체 자신** 을 지칭하는 구문이 됩니다.

그렇다면 객체를 따로 선언하지 않고 바깥에서는 사용할 경우 무엇을 지칭하게 될까요?

### global 객체에서의 사용법
```javascript
function print() {
  if (this === window) console.log('this is window');
  if (this === global) console.log('this is global');
}
print()
// browser 에서 실행할 경우 // this is window
// node.js 에서 실행할 경우 // this is global
```

이번에는 print()라는 함수를 바깥으로 꺼내 정의 후 실행해 보았습니다. this 라는 구문은 자신이 소속된 곳을 지칭하는 구문이기 때문에 이 경우도 역시 마찬가지로 자신이 속한 객체를 지칭합니다. 그리고 이 객체는 브라우서에서 실행할 경우는 **window** , node.js에서 실행할 경우는 **global** 객체를 지칭하게 됩니다.

사실 눈에 보이지는 않지만 우리가 선언하는 모든 객체는 상위 객체에 소속하게 됩니다. print() 라는 함수를 선언할 경우 정확이 얘기하자면 window.print() 처럼 상위객체인 window 객체에 속한 메소드로 정의 됩니다.