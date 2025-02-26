# Chapter-8 제어문

---

## 블록문, 고차함수, 제어문, for 문 중요
- 블록문(Block Statement)은 하나 이상의 문(statement)을 중괄호 `{}`로 묶은 것.
- 블록문의 끝에는 **세미콜론(;)을 붙여야 함**.
- 제어문(Control Statement)은 코드의 실행 흐름을 제어하는 문으로, 조건문과 반복문이 이에 해당.
- 고차 함수(Higher-order Function)는 **다른 함수를 인자로 받거나 반환하는 함수**로, 콜백 함수와 함께 자주 사용됨.

---

## 조건문: if
- `if` 문을 사용하여 특정 조건이 참(`true`)일 때 실행할 코드 블록을 정의.
- 만약 조건식이 **불리언 값이 아닌 값**으로 평가되면, **암묵적으로 강제 변환(Boolean 타입으로 변환)** 되어 실행할 코드 블록을 결정.
  - 예) `if ('hello') { console.log('실행됨'); }` → `"hello"`는 Truthy 값이므로 실행됨.
- `else if`, `else`는 옵션으로, **필요할 경우에만 추가적으로 사용** 가능.

### 예제 코드
```javascript
let score = 85;
if (score >= 90) {
    console.log("A 학점");
} else if (score >= 80) {
    console.log("B 학점");
} else {
    console.log("C 학점");
}
```

---

## break?
- `break` 문은 **반복문(for, while, do-while)과 switch 문에서 실행 흐름을 즉시 종료**할 때 사용.
- **폴스루(Fallthrough)**: `switch` 문에서 `break` 문이 없으면 다음 case로 넘어가는 현상.

### 폴스루를 이용하면 좋은 예시:
- 여러 case에서 같은 코드 블록을 실행할 경우 **break 없이 fallthrough**를 활용.
```javascript
let day = "토요일";
switch (day) {
    case "월요일":
    case "화요일":
    case "수요일":
    case "목요일":
    case "금요일":
        console.log("평일입니다.");
        break;
    case "토요일":
    case "일요일":
        console.log("주말입니다.");
        break;
    default:
        console.log("잘못된 입력입니다.");
}
```

---

## 반복문
- 반복문에는 **for, for...of, for...in, forEach** 등이 존재.
- `for` 문에서의 `i`는 **iteration(반복)의 i**를 의미.

### 기본적인 `for` 문
```javascript
for (let i = 0; i < 5; i++) {
    console.log(i);
}
```

### `for...of` 문 (배열 요소 순회)
```javascript
const fruits = ["사과", "바나나", "포도"];
for (const fruit of fruits) {
    console.log(fruit);
}
```

### `for...in` 문 (객체의 속성 순회)
```javascript
const user = { name: "Alice", age: 25, city: "Seoul" };
for (const key in user) {
    console.log(`${key}: ${user[key]}`);
}
```

### `forEach` (배열 전용 반복문, 콜백 함수 사용)
```javascript
const numbers = [1, 2, 3, 4, 5];
numbers.forEach(num => console.log(num));
```

---

## 무한 루프
- 종료 조건을 설정하지 않으면 반복문은 **무한히 실행**될 수 있음.
- 무한 루프는 일반적으로 **특정 조건에서 break 문을 이용해 종료**함.

### 잘못된 무한 루프 예시 (실행하면 브라우저 멈출 수 있음)
```javascript
while (true) {
    console.log("무한 루프");
}
```

### 정상적인 무한 루프 예시 (break 활용)
```javascript
let count = 0;
while (true) {
    console.log(count);
    if (count >= 10) break;
    count++;
}
```

---

## `break` 문과 레이블 문
- **break**: 현재 실행 중인 반복문 또는 switch 문을 **즉시 종료**.
- **레이블 문(Label Statement)**: 중첩된 반복문을 한 번에 탈출할 때 사용.

### `break` 예제
```javascript
for (let i = 0; i < 5; i++) {
    if (i === 3) break;
    console.log(i); // 0, 1, 2 출력 후 종료
}
```

### 레이블 문과 `break`
```javascript
outerLoop: for (let i = 0; i < 3; i++) {
    for (let j = 0; j < 3; j++) {
        if (i === 1 && j === 1) break outerLoop;
        console.log(i, j);
    }
}
// (0,0), (0,1), (0,2), (1,0)까지만 실행됨.
```

---

## 중첩 `for` 문
- `for` 문 안에 또 다른 `for` 문을 사용할 수 있음.

### 예제: 구구단 출력
```javascript
for (let i = 2; i <= 9; i++) {
    for (let j = 1; j <= 9; j++) {
        console.log(`${i} x ${j} = ${i * j}`);
    }
}
```

---

## JavaScript의 문자열은 배열?
- **JavaScript에서 문자열은 배열처럼 접근 가능**하지만, **불변(immutable) 특성을 가짐**.
- 문자열은 `for...of` 문을 사용하여 문자 단위로 순회 가능.

### 예제: 문자열 순회
```javascript
const str = "Hello";
for (const char of str) {
    console.log(char);
}
// H, e, l, l, o
```

### 하지만 문자열은 수정이 불가능!
```javascript
let str = "hello";
str[0] = "H"; // 변경되지 않음!
console.log(str); // "hello" 그대로 출력됨.
```

