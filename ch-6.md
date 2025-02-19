# Chapter 6 - 데이터 타입

## Infinity를 정의하는 두 가지 방법

- Infinity 전역 변수
    
    ```jsx
    console.log(Infinity); // Infinity
    console.log(typeof Infinity); // "number"
    ```
    
    - JavaScript에서 기본적으로 제공되는 전역 변수
    - 수학적인 무한대 값을 나타냄
    - 모든 숫자 연산에서 `Infinity`가 자동으로 사용됨
    - 재정의 가능
    
    ```jsx
    console.log(1 / 0); // Infinity (자동으로 전역 Infinity 사용)
    console.log(-1 / 0); // -Infinity
    ```
    
- Number.POSITIVE_INFINITY
    
    ```jsx
    console.log(Number.POSITIVE_INFINITY); // Infinity
    console.log(typeof Number.POSITIVE_INFINITY); // "number"
    ```
    
    - **`Number` 객체의 상수로 정의된 무한대 값**
    - `Infinity`와 동일하지만, **전역 변수와는 다르게 재정의할 수 없음**
    - 명확한 의미 전달 (예: `Number.POSITIVE_INFINITY` vs `Number.NEGATIVE_INFINITY`)
    - 재정의 불가능
    
    ⇒ Number.POSITIVE_INFINITY or Number.NEGATIVE_INFINITY 가 좀더 명확하다
    
    ⇒ But, Infinity가 더 간단
    

---

## typeof 와 instanceof

- typeof 피연산자 → 피연산자의 타입을 문자열로 반환한다.
    
    ```jsx
    console.log(typeof "Hello");    // "string"
    console.log(typeof 42);         // "number"
    console.log(typeof true);       // "boolean"
    console.log(typeof undefined);  // "undefined"
    console.log(typeof Symbol());   // "symbol"
    
    console.log(typeof null); // "object" (커버 안됨)
    console.log(typeof {}); // "object"
    console.log(typeof []); // "object" (Array인지 구별 불가능)
    console.log(typeof new Date());  // "object" (Date인지 구별 불가능)
    ```
    
    ⇒ 단점 모든게 typeof로 커버되지 않는다
    
- 왜?
    - PRIMITIVE(원시형) VS REFERENCE(참조형)에 해당되는데
    - 대부분은 PRIMITIVE 하지만 Array, Function, Date 같은 Object(REFERENCE)는 typeof로 감별되기 어렵다.
    - typeof Null → object가 된다 ⇒ Javscirpt에서 발생하는 언어적인 오류
    - 자바스크립트는 동적이기에  타입도 동적이다.
- instanceof
    
    이 연산자를 활용해서 객체의 프로토타입 체인을 검사하는 것
    
    이 객체에 대해 확인하기 위해 용이하다.
    
    ⇒ Array,Function,Date 사용시 용이하다.
    
    ```jsx
    console.log([] instanceof Array);       // true
    console.log(new Date() instanceof Date); // true
    console.log(function(){} instanceof Function); // true
    console.log({} instanceof Object);       // true
    ```
    

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