---
layout: post
title: Javascript - TDD로 개발하기 02 - Jasmin Framework
date: 2018-09-03 00:04:47 +0900
description: TDD-02 자스민 프레임워크의 기본 사용법
img: javascript.png
tags: [javascript, TDD]
---
---

## 자스민 이란?

자스민은 **자바스크립트 테스트 프레임워크** 로, Mocha 등과 같이 가장 많이 사용되는 프레임워크중 하나입니다.

## 기본 설치법

`npm install --save-dev jasmine` 로 설치하거나,
[링크](https://github.com/jasmine/jasmine/releases) 를 통해 소스파일(zip 파일)을 다운받아 사용할 수도 있습니다.

<br/>
## 기본 사용법

간단한 기본 사용법만 일단 확인 하기 위해 zip 파일을 다운받았다는 전제로 설명하겠습니다.<br/>

파일 압축을 풀고나면 SpecRunner.html 샘플 코드가 있습니다.

```html
<link rel="shortcut icon" type="image/png" href="lib/jasmine-2.7.0/jasmine_favicon.png">
<link rel="stylesheet" href="lib/jasmine-2.7.0/jasmine.css">

<script src="lib/jasmine-2.7.0/jasmine.js"></script>
<script src="lib/jasmine-2.7.0/jasmine-html.js"></script>
<script src="lib/jasmine-2.7.0/boot.js"></script>
```

사용할 자스민 스크립트 파일을 추가하고 하면 이제 자스민 프레임워크로 테스트용 코드를 작성할 수 있습니다.

```javascript
function sayHello(name) {
  return `hello ${name}`
}

describe('sayHello()', ()=> {
  it('전달한 이름에게 인사한다', ()=> {
    const name = 'Chris'
    expect(sayHello(name)).toBe(`hello ${name}`)
  })
})
```

하나씩 살펴보겠습니다.

- **describe** => test Suite(테스트 모음)<br/>
  여러 테스트를 묶어놓는 함수입니다.<br/>
  아래의 **it** 으로 구현되는 **test unit** 을 여러개 가질 수 있습니다. 보통 하나의 함수를 테스트하는 단위로 사용됩니다.<br/>
  **descrive** 함수는 부모 **descrive** 함수를 가질 수 있습니다.<br/>

- **it**(테스트 유닛)<br/>
  앞서 말씀드린 것처럼 하나의 작은 테스트 단위 입니다.<br/>
  첫번째 인자로 테스트 내용을 서술하고, 두번째 인자로 테스트 함수를 작성합니다.<br/>

- **expect**(결과값), **toBe**(기대값)<br/>
  영어의 문법 그대로를 표현해 놓은듯이 매우 직관적입니다.<br/>
  **expect**에 테스트 결과값이, **toBe** 에 test결과의 예상값이 들어갑니다.<br/>