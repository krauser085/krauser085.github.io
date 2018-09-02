---
layout: post
title: Javascript - fetch api
date: 2018-09-01 19:04:42 +0900
description: XMLHttpRequest 를 대체할 fetch api 알아보기
img: javascript.png
tags: [javascript]
---

---
참조 : https://developers.google.com/web/ilt/pwa/working-with-the-fetch-api

그동한 비동기로 서버에서 리소스를 받거나, SPA 개발시 AJAX 로 화면을 렌더링할 때
브라우저에서 제공하는 XMLHttpRequest 를 사용하거나, XMLHttpRequest의 불편함을 해소하기 위해 Jquery 의 Ajax 같은 라이브러리 등이 흔히 사용되어 왔습니다.

하지만 비교적 최신사양인 **fetch api** 를 통해서 좀 더 편한 방법으로 개발할 수 있게 되었습니다.<br/>

fetch api 는 매우 **추상적** 이고 **쉽게 구현 할 수 있게** 설계되었습니다.

<br/>
간단한 사용예를 보겠습니다.

## 기본적인 fetch 의 사용법

```javascript
fetch('리소스URL')
  .then(res => // response 객체)
  .catch(err => throw Error(err))
```

놀랍도록 심플합니다!!!

fetch 는 기본적으로 Promise 를 리턴합니다.<br/>
그리고 Promise 의 Then() 메소드의 파라미터로 서버로부터 response 객체를 돌려받습니다.<br/>

404 같은 bad request 의 경우, catch() 에서 처리되는 거 아닌가? 라고 생각 하실 수 있겠지만
google develop 의 document 에 따르면 request 가 완료되지 않은 경우(통신이 끊기거나 시간이 경과된 경우) 에만
catch() 메소드를 통해 처리된다고 합니다.

<br/>
이번에는 **Response** 객체가 가지고 온 리소스에 접근하는 방법에 대해서 알아보겠습니다.<br/>

**Json 객체를 요청하는 request 의 경우**, Response의 **json()** 메소드를 통해 리소스에 접근할 수 있습니다.

```javascript
fetch("examples/example.json")
  .then(res => res.json())
  .then(json => console.log(json));
```

위의 예처럼 **Response.json()** 메소드는 다시 **Promise** 를 반환합니다. <br/>

그리고 반환된 **Promise** 의 then() 메소드의 파라미터를 통해 **JSON** 값을 확인할 수 있습니다. <br/>
Promise 체이닝으로 구현되기 때문에 가독성도 향상되었습니다.<br/>
JSON 이외의 리소스 접근에서도 비슷한 방식으로 구현 할 수있습니다.<br/>
<br/>
이번에는 미디어 리소스와 텍스트 리소스를 가져오는 예를 살펴보겠습니다.

```javascript
// 이미지 파일, PDF 와 같은 미디어 리소스의 경우
fetch("examples/example.jpg")
  .then(res => res.blob())
  .then(blob => {
    // dom element에 blob 데이터 넘겨주기
    let el = document.querySelector("img");
    el.src = URL.createObjectURL(blob);
  });

// html, txt의 경우
fetch("examples/example.html")
  .then(res => res.text())
  .then(text => console.log(text));
```

위의 예처럼 리소스 형식에 관계없이 Response 객체의 text(), blob(), json() 메소드 모두 Promise 를 반환하기 때문에 구현방법은 동일합니다.

## HTTP 메소드 설정하기

fetch api 는 두번째 옵션 파라미터를 통해서 HTTP 메소드를 지정하거나 추가적인 설정이 가능합니다.

```javascript
fetch("someurl/comment", {
  method: "POST",
  body: "title=hello&message=world"
});

// Assuming an HTML <form> with id of 'myForm'
fetch("someurl/comment", {
  method: "POST",
  body: new FormData(document.getElementById("myForm"))
});

// 헤더 설정하기
var myHeaders = new Headers({
  "Content-Type": "text/plain",
  "X-Custom-Header": "hello world"
});

fetch("/someurl", {
  headers: myHeaders
});
```

<br/>
## Cross Origin Resource Sharing(CORS) 설정

CORS 관련 설정의 경우 mode 프로퍼티를 통해서 설정할 수 있습니다.<br/>
설정값은 3가지입니다.
1. **same-origin**<br/>
  같은 도메인 안에서만 리퀘스트<br/>
  same-origin 으로 설정되어 있는 상태에서 다른 도메인의 리소스를 요청할 경우 에러가 발생합니다.
2. **no-cors**<br/>
  cors 규정에 위배되지 않는 선에서 헤더를 보냅니다.<br/>
  받은 Response 객체도 Opaque 타입의 객체로 Response 의 어떠한 프로퍼티에도 접근할 수 없습니다.<br/>
3. **cors(default)**<br/>
  cors 요청으로 보냅니다.<br/>
  요청을 보낸 서버가 허용할 경우에만 Response를 받을 수 있습니다. 그렇지 않을 경우 에러가 발생합니다.

참고로 아래의 경우는 CORS 제약의 예외가 되는 조건입니다.<br/>
메소드가 GET, POST, HEAD 중 하나이면서
content-type이<br/>
- application/x-www-form-urlencoded
- multipart/form-data
- text/plain<br/>

중 하나의 경우는 예외입니다.

```javascript
// From http://foo.com/
fetch("http://bar.com/data.json", {
  mode: "no-cors" // 'cors' by default
})
.then(function(response) {
  // Do something with response
});
```

<br/>
## IE11에서 fetch API 사용하기

IE11 는 fetch 를 지원하지 않기 때문에 (참조: https://caniuse.com/#search=fetch) fetch api 를 사용하기 위해서는 polyfill 라이브러리를 사용해야 합니다.

가장 많이 사용하는 fetch polyfill 라이브러리는 github 에서 제공하는 fetch 라이브러리 입니다.

> https://github.com/github/fetch

가장 쉬운 방법으로 IE에서 구현하는 방법을 소개합니다.

1. github에서 파일을 직접 다운받거나 `npm install whatwg-fetch --save` 을 통해 설치합니다. (ver. 1.1)

2. index.html에 다운받은 fetch.js 파일을 스크립트 추가합니다.

```html
  <script src="https://cdn.jsdelivr.net/npm/promise-polyfill@7/dist/polyfill.min.js"></script>
  <script src="fetch.js"></script>
```

fetch 는 기본적으로 promise 를 리턴합니다.<br/>
하지만 IE11 는 이 Promise 기능도 지원하지 않기 때문에 Promise의 polyfill 도 추가하였습니다.<br/>

또 주의할점은 fetch polyfill 버전 1.1 이후의 경우 import, export의 모듈방식으로 구현됩니다.<br/>
네.. 역시 IE11는 이것도 지원하지 않기 때문에 추가적으로 라이브러리가 또 필요하게 됩니다... ㅠㅠ<br/>
간단하게 IE11에서 구현해보시려면 1.1 버전으로 사용하시면 됩니다.