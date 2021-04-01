---
marp: true
---

# **Poapper Backend Seminar**

<br>

## 2021-spring week2
컴공 18 최정원

---

# :bulb: 기명함수와 익명함수
- 기명함수는 RunTime 이전에 선언 / 익명함수는 RunTime에 동적으로 선언됩니다.
- 기명함수의 함수명은 함수 내부에서 자기 자신을 호출할 때 사용합니다.

<br>

+) 함수 선언식으로 선언한 경우, JS 엔진에 의해 코드가 다음과 같이 변경됩니다.
```javascript
function square(number) {
    return number * number;
}

var square = function square(number) {
    return number * number;
}
```

---

# 화살표 함수
JS에서 **익명함수**를 선언할 때 다음과 같이 `function` 키워드 대신에 `=>`를 사용하여 간단하게 표현할 수 있습니다.
```javascript
var square = function(num) {
    return num * num;
}

var square = (num) => {
    return num * num;
}

var square = num => {
    return num * num;
}
```
화살표 함수를 사용하면, 코드를 간단하게 작성할 수 있고 callback function이나 내부함수에 이용하기 좋습니다.

---

# 함수 호이스팅
**함수 선언문**을 이용하여 함수를 선언하였을 때, 함수 선언문이 작성된 위치와 관계없이 함수를 사용할 수 있습니다. -> 호이스팅이 일어나 함수 선언문이 최상단으로 끌어올려진 듯이 작동하였기 때문
```javascript
let sqaure_side = 5;
let square_area = square(square_side);

function square(number) {
  return number * number;
}
```

---

# 변수 호이스팅(1)
**모든 변수는 호이스팅**이 일어납니다. 하지만, 변수의 생성과정(1. 선언 단계, 2. 초기화 단계, 3. 할당 단계)에서 `var`는 1, 2가 동시에 일어나 호이스팅이 일어난 후 바로 참조 가능하지만 `let`과 `const`는 초기화가 되지 않았기 때문에 참조할 수 없습니다.
```javascript
console.log(x);     //undefined
console.log(y);     //Cannot access 'y' before initialization
console.log(z);     //Cannot access 'z' before initialization

var x = 'var';
let y = 'let';
const z = 'const';
```
```javascript
x = 'var';
console.log(x);     //var
var x;
```

---

# 변수 호이스팅(2)
변수 호이스팅이 일어났을 때 예측하지 못한 결과가 나타날 수 있습니다.
```javascript
for(var i = 0; i < 10; i++){

}
console.log(i)    //10
```
```javascript
var i;
for(i = 0; i < 10; i++){

}
console.log(i)    //10
```
_따라서 호이스팅을 최대한 피하기 위해 `var`나 `함수선언식`을 사용할 경우, 가급적 코드의 상단부에 선언하고, `let`이나 `const` 사용을 통해 혼선을 방지하는 것이 좋습니다._

---

# Synchronous vs. Asynchronous

<br>

동기식 처리(Synchronous)
```javascript
console.log("1st")
console.log("2nd")
console.log("3rd")
```
비동기식 처리(Asynchronous)
```javascript
console.log("1st")
setTimeout(() => {
  console.log("2nd");
}, 3000)    //ms 단위
console.log("3rd");
```
_*함수에 parameter로 전달되는 함수를 callack함수라 부릅니다._

---

# Synchronous vs. Asynchronous

<br>

![w:900](img/synchronous.png)


![w:900](img/asynchronous.png)

---

# Callback Hell
```javascript
asnyc1(() => {
  async2(() => {
    async3(() => {
      async4(() => {
        console.log("작업 완료???");
      })
    })
  })
})
```

---

# Promise
비동기 처리에서 사용되는 **객체**로, **pending**, **fulfilled**, **rejected**의 3가지 상태를 갖습니다.
```javascript
new Promise();      //pending

new Promise(function(resolve, reject) {

})

new Promise(function(resolve, reject) {
  resolve();
})

new Promise(function(resolve, reject) {
  reject();
});
```
`resolve()`를 호출하면 이행(Fulfilled)상태가 되고, `reject()`를 호출하면 실패(Rejected)상태가 됩니다.

---

Fulfilled)
```javascript
function getData() {
  return new Promise(function(resolve, reject) {
    var data = 100;
    resolve(data);
  });
}

// resolve()의 결과 값 data를 resolvedData로 받음
getData().then(function(resolvedData) {
  console.log(resolvedData); // 100
});
```
Then은 `promise.then(successCallback, failureCallback)`와 같이 콜백함수를 인자로 받음

---

Rejected)
```javascript
function getData() {
  return new Promise(function(resolve, reject) {
    reject(new Error("Request is failed"));
  });
}

// reject()의 결과 값 Error를 err에 받음
getData().then().catch(function(err) {
  console.log(err); // Error: Request is failed
});
```

---

예시1)
```javascript
new Promise(function(resolve, reject){
  setTimeout(function() {
    resolve("fulfilled!!");
  }, 2000);
})
.then(function(result){
  console.log(result);
});
```

---

예시2)
```javascript
function getData() {
  return new Promise(function(resolve, reject) {
    reject('failed');
  });
}

// 1. then()의 두 번째 인자로 에러를 처리하는 코드
getData().then(function() {
  // ...
}, function(err) {
  console.log(err);
});

// 2. catch()로 에러를 처리하는 코드
getData().then().catch(function(err) {
  console.log(err);
});
```

---

# 모듈화
`.js` 파일에 각각 코드를 분리함으로써 모듈화를 진행할 수 있습니다. 다음 코드의 모듈화를 진행해보면서 방법을 자세히 살펴보도록 하겠습니다.
```javascript
const PI = 3.14
const square = (num) => {
  return num * num;
}
const getCircleArea = (radius) => {
  return 0.5 * PI * square(radius);
}

console.log(`radius: ${3}, Circle Area ${getCircleArea(3)}`);
```

---

`circle.js`
```javascript
const PI = 3.14
const square = (num) => {
  return num * num;
}
const getCircleArea = (radius) => {
  return 0.5 * PI * square(radius);
}

exports.getArea = getCircleArea;
```

`main.js`
```javascript
const circle = require('./circle');

console.log(circle);            // { getArea: [Function: getCircleArea] }
console.log(circle.getArea(1)); // 1.57
```

---

# require과 라이브러리
JS에서는 require를 통해 라이브러리를 로드할 수 있습니다.
```javascript
const fs = require('fs');
const myProfile = fs.readFileSync('myProfile.json')
const myProfileJSON = JSON.parse(myProfile);

console.log(myProfileJSON);
console.log(myProfileJSON.name);
```
`readFileSync()`: String으로 파일을 읽어옴
`JSON.parse()`: String to JSON

---

# Homework :memo:

---

# HW2(Due: ~4/4 23:59:59)
_목적) 비동기 처리 사용해보기 / 라이브러리 사용해보기_

<br>

**1. 타이머**
`setInterval()` 함수를 이용하여 3초마다 'Hello World'를 출력하는 프로그램 만들기

<br>

**2. 전공책 JSON**
fs 라이브러리의 `writeFileSync()`를 이용하여, 전공책의 JSON 파일 만들기

---

# 질문 있나요? :eyes:

---

# 수고하셨습니다 :clap:
