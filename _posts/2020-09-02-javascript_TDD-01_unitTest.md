---
layout: post
title: Javascript - TDD로 개발하기 01 - Dependency Injection
date: 2018-09-02 20:45:49 +0900
description: Javascript 에서 TDD로 개발하기
img: javascript.png
tags: [javascript, TDD]
---

---

**TDD** 로 개발하기 위해서는 먼저 **Unit Test** 에 대해서 알아야 합니다.<br/>
**Unit Test** 는 작은 기능단위 혹은 함수 단위 테스트를 말합니다.<br/>

이 **Unit Test** 에 적합한 함수 구조를 만들기 위해서는 **DI(Dependency Injection)** 를 사용해 **테스트 하기 적합한 함수**를 만들어 주는 것이 일반적 입니다.

아마 자바로 웹 개발하시는 분들은 DI 에 대해서 잘 알고 계실꺼라 생각합니다. (DI 가 Spring 의 핵심이 되는 걔념이기 때문에)<br/>

오늘은 **Unit Test** 를 수월하게 만들어주는 **Dependency Injection** 에 대해서 알아보겠습니다.

<br/>
## Dependency Injection 이란?

**Dependency Injection** 을 번역하면 **의존 주입** 이라는 말로 번역할 수 있습니다.<br/>
조금더 길게 설명하자면 함수가 **의존하고(사용하고)** 있는 객체들을 함수의 **프로퍼티** 로 **주입**하는 방법을 이야기 합니다.

예를 가지고 살펴보겠습니다.

```javascript
function getUserName(userId) {
  fetch("user/" + userId)
    .then(res => res.text())
}
```

위의 함수는 유저 정보를 가지고 프로미스로 유저 이름을 반환하는 함수 입니다.<br/>
이 함수 안에는 `window.fetch()` 함수가 사용되고 있습니다. 함수가 이 fetch() 함수를 사용하고 있다는 건 **fetch() 함수에 의존하고 있다**는 뜻입니다.
> [**fetch 함수 알아보기**](/javascript_fetch/)

<br/>
**Unit Test** 를 하게 되면 보통 테스트 용 데이터를 넘겨주어 결과를 확인하게 됩니다.<br/>
하지만 처음의 예처럼 **getUserName** 함수가 **fetch** 를 의존하고 있으면, 테스트용 **UserId** 데이터를 넘기더라고 **Window.fetch()** 함수는 그대로 실행되게 됩니다.<br/>
**fetch()** 함수는 서버에 정의된 유저 **리소스를 로드**하게 되고 **getUserName** 함수만 테스트 하고자 했던 UnitTest 의 의미는 사라지고, 결과적으로 서버와의 통합테스트가 되버리는 결과를 초래합니다. ㅠㅠ<br/>

그렇다면 **Dependency Injection** 으로 어떻게 이 문제를 해결할 수 있을까요?
이번에는 **Dependency Injection** 으로 **함수를 리펙토링** 해보겠습니다.

```javascript
function getUserName(fetch, userId) {
  return fetch("user/" + userId)
    .then(res => res.text())
}
```

위와 같이 **fetch()** 함수를 **getUserName** 함수의 파라미터로써 넘겨주었습니다.<br/>

이렇게 하게 되면 이제 테스트용 데이터를 넘겨줄때 **userId**, 뿐만 아니라 **test 용 fetch** 함수도 넘겨줄 수 있게 되었습니다.<br/>

마지막으로 테스트용 가짜 데이터를 넘겨줘서 원하는 결과가 나오는 것 까지만 살펴보겠습니다.

```javascript
// test용 fetch 함수
var testFetch = () => {
  return new Promise(res => {
    res({
      text: () => Promise.resolve("David")
    })
  })
}

getUserName(testFetch, "1234")
  .then(name => console.log(name)) // David
```

위처럼 가짜 함수를 넘겨줌으로써 (**Injection**) 온전히 **getUserName 안에서만의 UnitTest가 가능**하게 되었습니다.

이렇게 해서 TDD에 대해 본격적으로 시작하기전에 필수적으로 알아야하는 걔념인 DI 와 UnitTest 에 대해서 알아보았습니다.