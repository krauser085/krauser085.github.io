---
layout: post
title: Javascript - TDD로 개발하기 02 - Jasmin Framework
date: 2018-09-03 00:04:47 +0900
description: TDD-02 자스민 프레임워크의 기본 사용법
img: tdd.gif
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

<br/>
## DOM element 테스트 케이스 작성하기

이번에는 DOM element 의 테스트 케이스를 알아보겠습니다.
DOM element 를 테스트 하는 경우에는 대상 element를 주입하는 형식으로 테스트 케이스를 작성할 수 있습니다.

```javascript
function sayHello(element, name) {
  return element.innerText = `Hello ${name}`
}

describe('sayHello()', ()=> {
  it('전달한 이름을 화면에 출력한다', ()=> {
    const
      element = document.querySelector('span'),
      name = 'YD'
      sayHello(element, name)
    expect(element.innerText).toBe(`Hello ${name}`)
  })
})
```
컨트롤러나 뷰모델을 통해서 DOM이 관리되는 식이라면 더 바람직한 코드가 되겠지만 확인차원에서 간단하게 작성해 보았습니다.

이번에는 파라미터 변수를 체크하는 테스트 케이스를 추가해 보도록 하겠습니다.

<br/>
## 파라미터 체크 테스트 케이스

실행 함수에서 파라미터를 체크하고 유효하지 않을 경우 **throw** 로 던져주는 식으로 작성해 보겠습니다.

```javascript
function sayHello(element, name) {
  if (!element) throw new Error('유효하지 않은 element 입니다.')
  if (!name) throw new Error('name 이 없습니다.')

  element.innerText = `Hello ${name}`
}

describe('sayHello()', ()=> {
  const element, name

  beforeEach(() => {
    element = document.querySelector('span')
    name = 'YD'
  })

  it('element 를 주입하지 않을경우 에러가 발생한다', () => {
    expect(sayHello(null, name)).toThrowError()
  })
  it('name 를 주입하지 않을경우 에러가 발생한다', () => {
    expect(sayHello(element, null)).toThrowError()
  })
  it('전달한 이름을 화면에 출력한다', ()=> {
    sayHello(element, name)
    expect(element.innerText).toBe(`Hello ${name}`)
  })
})
```

함수에 주입되는 파라미터를 체크하는 **it** 테스트 케이스가 2개 추가 되었습니다. 그리고 element 와 name 변수는 공통으로 사용되기 때문에 beforeEach로 각 테스트가 실행되기전 전처리기로 설정해 주었습니다.

에러가 발생하는 부분에서 실행 함수가 **throw** 로 에러를 던지면 **toThrowError** 는 에러가 던져질 것을 예상해서 **true** 를 반환하게 됩니다.

<br/>
## 함수 감시하기(spyOn)

jasmin 에서는 **spyOn** 함수를 이용해 특정함수의 실행여부를 확인할 수 있습니다.

```javascript
const getView = function (element, name) {
  return {
    setElementText(text) {
      element.innerText = text
    }
    sayHello() {
      this.setElementText(`Hello ${name}`)
    }
  }
}

describe('view 모듈의' () => {
  const element, name, view

  beforeEach(() => {
    element = document.querySelector('span')
    name = 'YD'
    view = getView(element, name)
  })

  describe('sayHello() 함수는', ()=> {
    it('view 모듈의 setElementText() 를 실행한다', () => {
      spyOn(view, 'setElementText')
      view.sayHello()
      expect(view.setElementText).toHaveBeenCalled()
    })
  })
})
```

**spyOn** 메소드는 첫번째 인자로 모듈명을, 두번째 인자로 모듈의 메소드명을 받기 때문에 sayHello() 메소드를 포함하는 모듈을 만들어 테스트 케이스를 만들어 보았습니다.<br/>
**spyOn** 으로 감시되는 메소드는 **toHaveBeenCalled()** 함수로 실행여부를 확인할 수 있습니다.