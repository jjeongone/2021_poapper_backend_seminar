---
marp: true
---

# **Poapper Backend Seminar**

<br>

## 2021-spring week1
컴공 18 최정원

---

# About Seminar(1)
- 출석체크는 **수업이 끝난 뒤**에 하도록 하겠습니다. 다들 시간 맞춰 들어와주세요!
- 질문은 언제든 편하게 음성/채팅을 이용해 주시면 됩니다.
- 카톡을 이용한 질문도 환영입니다
- **수업(0.5) + 숙제(0.5) = 출석(1.0)**
  - 수업에 참여하지 못하는 경우 미리 저에게 알려주시고, 수업 녹화본을 보신 뒤에 과제를 제출하시면 출석인정을 해드립니다.
- 결석 3회시 U
- 기말과제 완료시 S

---

# About Seminar(2) 
- 세미나에서는 개발에 필요한 최소한의 JS문법만을 다룹니다.
- 세미나는 여러분이 backend를 공부하는 방향성을 제시하는 것을 목표로 합니다.
- 수업 전 **반드시!** 미리 올려드리는 포스트를 읽고 와주세요.
- 수업이 끝나면?
    1. 숙제가 나갑니다 -> 직접 해보는 것이 최고의 복습!
    2. 추가적인 보충 포스트를 (가능한)게시할 예정입니다. -> 수업에서 다룬 것 + @

---

# 그럼 Backend Seminar를 시작해 보겠습니다! :tada:

---

# 변수
JavaScript에서는 `var`, `let`, `const` 키워드를 사용하여 변수를 선언합니다.
```javascript
var v1;
let v2;
const v3;
```

---

# 데이터 타입
JavaScript에서는 데이터타입을 크게 **두 가지**로 나눌 수 있습니다.
1. **기본 데이터 타입(primitive type)**: `Number`, `String`, `Boolean`, `undefined`, `null`
   변수에 저장하거나 함수에 전달할 때 데이터 값 자체가 복제됩니다.
   ```javascript
   var x = 100;        // 원시 타입 데이터를 선언
   var y = x;          // 값을 새 변수에 복사
   x = 99;             // 'x'의 값을 변경
   console.log(y);     // 100, 'y'의 값은 변경되지 않음
   ```
2. **참조 데이터 타입(reference type)**: `Object`, `Array`, `Function`
   변수에 저장하거나 함수에 전달할 때 데이터의 참조가 전달됩니다.
   ```javascript
   var x = { count: 100 }; // 참조 타입 데이터를 선언
   var y = x;              // 참조를 새 변수에 복사
   x.count=99;             // 참조 타입 데이터를 변경
   console.log(y.count);   // 99, 'x'와 'y'는 동일한 참조를 담고 있으며, 따라서 동일한 객체를 가리킴
   ```
---

# 비교연산자
1. `==` / `!=`: type conversion을 이용 -> **type이 달라**도 true값 반환
   ```javascript
   console.log(1 == 2); // false
   console.log(1 == "1"); // true
   console.log(0 == false); // true
   console.log(null == undefined); // true
   ```

<br>

2. `===` / `!==`: 변수의 **type까지 같아**야 true를 반환
    ```javascript
    console.log(1 === "1"); // false
    console.log(0 === false); // false
    console.log(null === undefined); // false
    ```

---

# 배열
JavaScript에서 배열은 `[]`을 통해 표현합니다.
```javascript
let arr1 = [1, 2, 3, 4];
let arr2 = [1, "two", 3, 4.0];
```

---

# 반복문
JavaScript의 반복문은 다음과 같이 사용합니다.
```javascript
let arr1 = [1, 2, 3, 4];
for(let i=0; i < arr1.length; i++){
  console.log(arr1[i]);
}
```
외에도 `while`문을 이용하여 반복문을 구현한 수 있습니다.

---

# 함수
JavaScript에서 함수는 다음과 같이 선언합니다.
```javascript
function square(number) {
  return number * number;
}
```
앞서 다루었듯이, JavaScript에서의 함수는 **변수**로 취급되고 다음과 같이 변수에 저장할 수 있습니다. 이러한 방식을 **함수 표현식**이라 합니다.
```javascript
let square = function(number) {
  return number * number;
}

let sqaure_side = 5;
let square_area = square(square_side);
```
위의 함수 표현식을 보면, 함수명이 생략되어 있음을 알 수 있는데, 이를 **익명함수**라 부릅니다.

---

# 객체
객체는 **프로퍼티(property)** 의 집합이고, 프로퍼티는 **키(kye)** 와 **값(value)** 의 쌍입니다.
```javascript
let member = {
  id: "user_id",
  pw: "123456789",
  role: "student", 
  func: square // 함수를 value로 저장
}
```

---

# 객체에 접근하기
1. 객체 인덱스 `[]` 이용하기
   ```javascript
   console.log(member["id"]);
   member["gender"] = "male";
   ```
2. `.` 이용하기
   ```javascript
   console.log(member.id);
   member.gender = "male";
   ```

---

# JSON
**JSON(JavaScript Object Notation)** 은 구조화된 정보를 저장하는 형식(foramt)입니다.
key-value의 쌍으로 구성되어 있으며, `.json` 형식으로 저장합니다.
```JSON
{
  "name": "hsy4462",
  "job": "student",
  "age": 22,
  "hobby": ["jazz", "steam game"],
  "course_table": [
    {"name": "computer vision", "id": "AIGS539"},
    {"name": "Software Design", "id": "CSED332"},
    {"name": "Modern Algebra 1", "id": "MATH301"},
    {"name": "응용복소함수론", "id": "MATH210"},
    {"name": "중영작", "id": "GEDU131"}
  ]
}
```
*서버가 프론트와 상호작용할 때 JSON형식으로 파일을 주고받습니다*

---

# Homework :memo:

---

# 잠깐 공지사항 있어요! :hand:
- 숙제는 제 **POVIS 메일**을 이용하여 제출하게 됩니다.
- 메일을 찾기 쉽도록 제목 양식을 통일해 주세요!
    > HW{homework_number}_{your_name}
    > ex) HW1_최정원
- 숙제 파일이 여러개인 경우 **zip**파일로 압축해서 보내주시면 됩니다.
- zip 파일의 제목도 위의 제목 양식과 동일하게 해주시면 좋을 것 같아요!

---

# HW1(Due: ~3/28 23:59:59)
_목적) JavaScript로 출력 해보기 / JavaScript의 함수 사용해보기 / JSON 사용해보기_

<br>

**1. 구구단 출력하기**
이중 for문을 이용하여 console에 구구단을 출력해보자!

**2. 피보나치 수**
자연수 n을 받아 피보나치 수의 값을 return하는 함수 `fibo()`를 만들어보자!

**3. myProfile.json 작성하기**
JSON형식에 맞추어 나의 프로필 작성하기! (다음 프로퍼티들이 포함되어야 함)
> name, job, age, hobby, course_table

*backend seminar week1 자료의 JSON파트에 예시가 있음*

---

# Q&A :thinking:

---

# 자문자답 Q&A :eyes:
:question: 왜 var, let, const가 다 필요할까?
:bulb: JavaScript의 Scope와 관련이 있는데, var만을 사용하면 **전역변수를 남발**할 수 있고, 긴 코드를 작성하다 실수로 중복되는 변수명을 선언하여 오류가 발생하면 **디버깅이 어려울** 수 있습니다.

<br>

:question: JSON과 Object(객체)의 차이?
:bulb: Object는 메모리에 저장하는 **데이터 구조**를 말하고, JSON은 **객체의 내용을 담는 파일**을 의미합니다.

<br>

:question: JavaScript에서는 ;(세미콜론)을 써야할까?
:bulb: JavaScript에는 **세미콜론 자동 삽입**기능이 존재하여, 굳이 세미콜론을 쓰지 않아도 오류 없이 코드가 실행됩니다. 세미콜론을 사용 여부에 대한 여러 주장들이 있지만, 좀더 명확한 코드를 위해 세미콜론을 작성하는 것도 나쁘지 않다고 생각합니다.


---

# 수고하셨습니다! :+1:
