# Ch-9 타입 변환과 단축 평가

---

## 자동 변환과 개발자의 의도
- JavaScript에서는 값의 타입이 **자동으로 변환(암묵적 타입 변환)** 되는 경우가 많음.
- 이러한 자동 변환은 **개발자의 의도가 코드에서 명확하게 드러나지 않게 만들 수 있음**.
- 따라서, 값이 어떻게 변환될지 예측 가능해야 하며, 이를 명확하게 하기 위해 **TypeScript(TS)를 사용하는 이유**가 됨.

### 예제: 문자열 변환
```javascript
var x = 10;
var str = x + ''; // 숫자가 문자열로 변환됨
console.log(typeof str, str); // string "10"
console.log(typeof x, x); // number 10
```
- `x + ''`는 **자동으로 문자열로 변환**됨.
- 하지만 개발자의 의도가 코드에서 명확히 드러나지 않으므로, `String(x)`를 사용하는 것이 더 좋음.

---

## 암묵적 타입 변환 (Implicit Type Conversion)
- JavaScript는 **연산자의 종류와 문맥(Context)에 따라 타입을 자동 변환**함.
- 예를 들어, `{}`는 객체지만 **`+ ''`를 만나면 문자열로 변환됨**.

### 예제: `{}` + '' 의 결과
```javascript
({}) + ''; // "[object Object]"
```
- `{}`는 객체이므로, 문자열과 더해질 때 `"[object Object]"`로 변환됨.

### `({}) + ''`를 `({})`로 만드는 방법?
```javascript
console.log(String({})); // "[object Object]"
console.log(JSON.stringify({})); // "{}"
```
- `String({})`를 사용하면 `"[object Object]"`로 변환.
- `JSON.stringify({})`를 사용하면 `"{}"`로 변환됨.

---

## 단항 `+` 연산자
- 단항 `+` 연산자는 **피연산자가 숫자 타입이 아닐 경우, 숫자로 변환하려고 시도**함.

### 예제:
```javascript
console.log(+"10"); // 10 (문자열 → 숫자 변환)
console.log(+true); // 1 (불리언 → 숫자 변환)
console.log(+false); // 0
console.log(+null); // 0
console.log(+undefined); // NaN
console.log(+{}); // NaN (객체는 숫자로 변환할 수 없음)
```

---

## `Number()` vs `parseInt()`
| 변환 함수 | 특징 | 예제 |
|---|---|---|
| `Number()` | 전체 값을 숫자로 변환 | `Number("10.5") → 10.5` |
| `parseInt()` | **문자열에서 정수 부분만 추출** | `parseInt("10.5") → 10` |
| | 첫 번째 숫자가 아닌 문자를 만나면 변환 종료 | `parseInt("10px") → 10`, `Number("10px") → NaN` |

### 예제:
```javascript
console.log(Number("10.5")); // 10.5
console.log(parseInt("10.5")); // 10
console.log(Number("10px")); // NaN
console.log(parseInt("10px")); // 10
```

---

## 왜 `Boolean({})` → `true`일까?
- JavaScript에서 **Falsy 값(거짓으로 평가되는 값)** 은 정해져 있음:
  - `false`, `0`, `-0`, `""`(빈 문자열), `null`, `undefined`, `NaN`
- 이외의 값은 **Truthy 값(참으로 평가되는 값)** 이므로, `{}`도 **Truthy** 값으로 평가됨.

### 예제:
```javascript
console.log(Boolean({})); // true (빈 객체도 truthy)
console.log(Boolean([])); // true (빈 배열도 truthy)
console.log(Boolean("")); // false (빈 문자열은 falsy)
console.log(Boolean(0)); // false (0은 falsy)
```

---

## 단축 평가 (Short-Circuit Evaluation)
- 논리 연산자 `&&`(AND)와 `||`(OR)를 사용할 때 **필요한 값만 평가하는 방식**.
- **불필요한 연산을 줄이는 데 사용**되며, **기본값을 설정하거나 값이 존재할 경우 특정 코드를 실행할 때 유용**.

### 논리곱(`&&`)
- **첫 번째 값이 `false`이면** 두 번째 값은 평가되지 않고 첫 번째 값이 반환됨.
```javascript
console.log(false && "hello"); // false
console.log(true && "hello"); // "hello" (true이므로 다음 값 반환)
```

### 논리합(`||`)
- **첫 번째 값이 `true`이면** 두 번째 값은 평가되지 않고 첫 번째 값이 반환됨.
```javascript
console.log(true || "hello"); // true
console.log(false || "hello"); // "hello" (false이므로 다음 값 반환)
```

### 예제: 기본값 설정
```javascript
let name = null;
let userName = name || "Guest";
console.log(userName); // "Guest" (name이 null이므로 기본값 할당)
```

---

## `!!` 연산자: 불리언 변환
- `!` 연산자를 두 번 사용하면 **값을 불리언으로 변환하는 효과**가 있음.

### 예제:
```javascript
console.log(!null); // true (null은 falsy)
console.log(!!null); // false (한 번 뒤집고 다시 뒤집음)
console.log(!!"hello"); // true (문자열은 truthy)
console.log(!!0); // false (0은 falsy)
```

## `!!`를 많이 사용할까?
- `Boolean()` 함수를 사용해도 같은 결과를 얻을 수 있음.
- `!!`는 **빠르고 간단하지만, 코드의 가독성이 떨어질 수 있음**.
```javascript
console.log(Boolean(null)); // false
console.log(!!null); // false
```
- **실제 코드에서는 `Boolean()`을 더 자주 사용**하지만, `!!`도 간단한 경우에는 활용 가능.

---

## 옵셔널 체이닝 연산자 `?.`
- 객체 프로퍼티에 접근할 때, 값이 `undefined` 또는 `null`이면 **오류를 발생시키지 않고 `undefined`를 반환**.

### 예제:
```javascript
const user = { name: "Alice" };
console.log(user?.name); // "Alice"
console.log(user?.age); // undefined (에러 발생 X)
```

### 옵셔널 체이닝을 사용하지 않은 경우:
```javascript
console.log(user.address.street); // 오류 발생! (address가 없음)
```

### 옵셔널 체이닝을 사용한 경우:
```javascript
console.log(user?.address?.street); // undefined (안전하게 처리)
```

