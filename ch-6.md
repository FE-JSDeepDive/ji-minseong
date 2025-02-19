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

## **타입관련 개념**

| 개념 | 설명 | 예제 |
| --- | --- | --- |
| **타입 캐스팅 (Type Casting)** | **프로그래머가 직접 변환 (명시적 변환)** | `Number("123")`, `String(123)`, `Boolean(0)` |
| **동적 타이핑 (Dynamic Typing)** | **변수의 타입이 실행 중 변경 가능** | `let x = 10; x = "Hello";` |
| **암묵적 타입 변환 (Implicit Type Conversion)** | **JavaScript 엔진이 자동 변환** | `"5" + 2 → "52"`, `"5" - 2 → 3` |
| **타입 강제 변환 (Type Coercion)** | **암묵적 타입 변환과 같은 개념 (예측 어려움)** | `1 == "1" → true`, `0 == false → true` |