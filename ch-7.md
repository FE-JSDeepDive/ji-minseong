# Chapter-7 연산자

---

## isNaN

- isNaN : is Not a Number
    
    ⇒ "Not a Number" (숫자가 아닌 값)를 의미하는 특수한 값
    => 하지만, "숫자가 아닐 때"가 아니라, "진짜 NaN 값일 때"만 true가 나옴
    

```jsx
console.log(isNaN(123)); // false (123은 숫자)
console.log(isNaN("123")); // false ("123"은 숫자로 변환됨)
console.log(isNaN("123abc")); // true ("123abc"는 숫자로 변환 불가 → NaN)
console.log(isNaN(true)); // false (true → 1로 변환)
console.log(isNaN(undefined)); // true (undefined → NaN으로 변환)
console.log(isNaN(null)); // false (null → 0으로 변환)
```

⇒ 따라서 `Number.isNaN` 으로 검사하는 것을 추천

```jsx
isNaN // 느슨한 검사
Number.isNaN // 엄격한 검사
```

```jsx
console.log(Number.isNaN(123)); // false (123은 숫자)
console.log(Number.isNaN("123")); // false ("123"은 NaN이 아님)
console.log(Number.isNaN("123abc")); // false ("123abc"는 NaN이 아님)
console.log(Number.isNaN(true)); // false (true는 NaN이 아님)
console.log(Number.isNaN(undefined)); // false (undefined는 NaN이 아님)
console.log(Number.isNaN(null)); // false (null은 NaN이 아님)
console.log(Number.isNaN(NaN)); // true (진짜 NaN일 때만 true)
```

| 연산자 | 동작 방식 | 타입 변환 | 추천 여부 |
| --- | --- | --- | --- |
| `isNaN(value)` | 느슨한 검사 | **O (자동 변환 발생)** | (사용 지양) |
| `Number.isNaN(value)` | 엄격한 검사 | **X (변환 없음)** |  (권장) |

---

## Object.is와 useEffect

(참고 : https://youtu.be/_9Uz3b6izuA?feature=shared)

`Object.is(a, b)`는 두 값이 **완전히 같은지(동일성 비교, Same Value Equality)** 판단하는 메서드

```jsx
console.log(Object.is(5, 5)); // true
console.log(Object.is("hello", "hello")); // true
console.log(Object.is({}, {})); // false (다른 객체)
console.log(Object.is(NaN, NaN)); // true (===과 차이점)
console.log(NaN === NaN); // false (기본 비교는 NaN을 다르게 봄)
console.log(Object.is(-0, 0)); // false (===과 차이점)
console.log(-0 === 0); // true (기본 비교는 -0과 0을 같게 봄)
```

=> React의 `useEffect()`는 의존성 배열([]) 내부 값이 변경될 때만 실행

⇒ 이때 React는 Object.is(a,b) 를 사용하여 이전 값(a)과 새로운 값(b)을 비교

---

## if-else 대신 Early Return

책에서 `조건문이 여러개라면 if ... else 문의 가독성이 더 좋다` 

⇒ early return 방식 고려 가능

- if-else
    
    ```jsx
    function checkAge(age) {
        if (age >= 18) {
            console.log("성인입니다.");
        } else {
            console.log("미성년자입니다.");
        }
    }
    ```
    
- early return
    
    ```jsx
    function checkAge(age) {
        if (age < 18) {
            console.log("미성년자입니다.");
            return;
        }
        console.log("성인입니다.");
    }
    ```
    
- if-else → 가독성 악화
    
    ```jsx
    // if-else 중첩 (읽기 어려움)
    function processUser(user) {
        if (user) {
            if (user.isActive) {
                if (user.age >= 18) {
                    return "성인 회원입니다.";
                } else {
                    return "미성년자 회원입니다.";
                }
            } else {
                return "비활성화된 계정입니다.";
            }
        } else {
            return "유효하지 않은 사용자입니다.";
        }
    }
    ```
    
- early-return
    
    ```jsx
    function processUser(user) {
        if (!user) return "유효하지 않은 사용자입니다.";
        if (!user.isActive) return "비활성화된 계정입니다.";
        if (user.age < 18) return "미성년자 회원입니다.";
    
        return "성인 회원입니다.";
    }
    ```
    

---

## 삼항 연산자 대신 switch

책에서 `if-else를 사용하는게 더 가독성이 좋다` 다른 방법으로 `switch`

```jsx
const userType = "admin";

const access = userType === "admin"
  ? "관리자 페이지 접근 가능"
  : userType === "user"
  ? "일반 사용자 페이지 접근 가능"
  : "접근 불가";

console.log(access);
```

⇒ 가독성이, 유지보수 하기에 좋지 않음

```jsx
const userType = "admin";
let access;

switch (userType) {
    case "admin":
        access = "관리자 페이지 접근 가능";
        break;
    case "user":
        access = "일반 사용자 페이지 접근 가능";
        break;
    default:
        access = "접근 불가";
}

console.log(access);
```

⇒  **조건이 많아질수록 가독성이 뛰어남, 각 case별로 명확하게 구분됨 → 유지보수 편리**