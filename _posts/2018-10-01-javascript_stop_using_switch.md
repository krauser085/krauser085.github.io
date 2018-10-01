---
layout: post
title: Stop using Switch
date: 2018-10-01 22:36:29 +0900
description: Switch 는 정말로 필요한가?
img: javascript.png
tags: [javascript]
---
---
프로그래머라면 항상 어떤 것이 더 효율적인 방법인지 고민할 필요가 있습니다. 항상 습관적으로 써오던 구문이나 라이브러리, 알고리즘 등도 더 좋은 방법이나 상황에 더 어울리는 쪽으로 바꿀 수 있는 가능성은 언제나 존재합니다.

이러한 맥락에서 **Switch** 구문에 대해서 생각해 보고자 합니다. <br/>
**switch** 구문은 프로그래밍 언어라면 기본적으로 if 와 함께 지원하고 있는 조건문 입니다.

일반적으로 알고 있듯이 if, else if 가 다량으로 중첩될 경우에는 switch 의 경우가 다량의 else if 보다 효율적인 경우가 많습니다.

```javascript
// if, else if 의 경우
function getDrink(beverage) {
  if (beverage === 'coke') {
    return 'I like to drink coke'
  }
  else if (beverage === 'juice') {
    return 'I like to drink juice'
  }
  else if (beverage === 'milk') {
    return 'I like to drink milk'
  }
  else if (beverage === 'coffee') {
    return 'I like to drink coffee'
  }
  else return "I don't like to drink anything"
}

// switch 의 경우
function getDrink(beverage) {
  switch (beverage) {
    case 'coke':
      return 'I like to drink coke'
      break
    case 'juice':
      return 'I like to drink juice'
      break
    case 'milk':
      return 'I like to drink milk'
      break
    case 'coffee':
      return 'I like to drink coffee'
      break
    default:
      return "I don't like to drink anything"
      break
  }
}
```

위와 같이 다수의 if else 의 조건문 보다는 switch 의 경우가 더 가독성이 향상되고 반복되는 조건에 비교값만 변경되는 것이기 때문에 성능적인 면에서도 더 좋다고 할 수 있습니다.

하지만 switch 문에서도 단점은 존재합니다.
1. case 마다 반복적으로 break 를 명시해야한다.(필요에 의해 뺄수도 있지만...)
1. javascript 가 지향하는 객체지향적인 모습이 아니다.
1. 매 조건마다 비교하고 다음 case 로 넘어가기 때문에 비효율적일 수 있다.

위와 같은 문제들 때문에 javascript 에서는 **object literals** 을 사용한 look up 방식이 더 효율적인 방법으로 여겨지고 있습니다.

위에서 살펴본 switch 문을 object literals 로 바꾸게 되면 아래와 같습니다.
```javascript
function getDrink(beverage) {
  return {
    coke: 'I like to drink coke',
    juice: 'I like to drink juice',
    milk: 'I like to drink milk',
    coffee: 'I like to drink coffee'
  }[beverage] || "I don't like to drink anything"
}

console.log(getDrink('milk')) // I like to drink milk
```

훨씬 **간결**해지고, **가독성도 향상**되며, 조건문의 실행 없이 hash table 에서의 검색이기 때문에 **속도도 훨씬 증가** 하였습니다.

결론적으로, 경우에 따라서는 switch 구문이 필요한 경우도 있겠지만, **대부분의 경우에는 object literals 구문으로 대체하는 것이 더 효율적인 방법이라고 할 수 있을 것 같습니다.**