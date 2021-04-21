---
marp: true
---

# **Poapper Backend Seminar**

<br>

## 2021-spring week3
컴공 18 최정원

---

# async/await

async/await을 이용하면, Promise를 보다 가독성 좋게 사용할 수 있습니다.

```javascript
async function f() {
    var result = await new Promise((resolve, result) => {
        setTimeout(resolve("fulfilled!!"), 2000);
    })
    console.log(result);        // fulfilled!
}
```

---

# async/await의 예외 처리

try-catch 문을 이용하여 error handling을 할 수 있습니다.

```javascript
async function f() {
    try {
        var result = await new Promise((resolve, result) => {
            setTimeout(resolve("fulfilled!"), 2000);
        })
        console.log(result);
    } catch(err) {
        console.log(err);
    }
}
```

---

# 지금부터 :star:진짜:star: 웹개발을 배워보도록 하겠습니다.

---

# Request-Response

![](img/request_response.png)

---

# HTTP module을 이용한 web server 만들기

## **H**yper**T**ext **T**ransfer **P**rotocol

---

# Homework :memo:

---

# HW3(Due: ~4/28 23:00:00)

_목적) 라이브러리 사용해보기 / 라우팅 서버 구현해보기_

<br>

**1. 타이머**
`localhost:8080/timer`에 접속하면 한국 시간을 기준으로 현재 시간을 브라우저에 출력하기

<br>

**2. Simple Calculator**
url을 이용해 간단한 계산기를 작성해보기

- 구현할 연산: 덧셈(add), 뺄셈(sub), 곱셈(mul), 나눗셈(div)
- url 형식
  - `localhost:8080/operator/num1/num2`
  - (ex) `localhost:8080/add/1/2`

---

# 질문 있나요? :eyes:

---

# 수고하셨습니다 :clap: