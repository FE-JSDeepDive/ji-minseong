## 1. `&&` 연산자의 단축 평가에 대해 설명하세요.

- 정답  
    - `&&` 연산자는 **첫 번째 값이 falsy이면 해당 값을 반환**하고, truthy이면 두 번째 값을 반환  
    - 첫 번째 값이 `false`, `0`, `""`, `null`, `undefined`, `NaN` 등의 falsy 값이면 평가가 중단됨  
    - 주로 조건이 참일 때 실행해야 하는 코드에서 활용  

- 예제  
    ```javascript
    console.log(false && "출력될까요?"); // false
    console.log(true && "출력됩니다!");  // "출력됩니다!"
    
    const isLoggedIn = true;
    isLoggedIn && console.log("로그인 성공!"); // "로그인 성공!" 출력
    ```

---

## 2. `||` 연산자의 단축 평가에 대해 설명하세요.

- 정답  
    - `||` 연산자는 **첫 번째 값이 truthy이면 해당 값을 반환**하고, falsy이면 두 번째 값을 반환  
    - 첫 번째 값이 truthy이면 평가가 중단됨  
    - 주로 기본값을 설정하는 데 활용  

- 예제  
    ```javascript
    console.log(true || "출력될까요?");  // true
    console.log(false || "출력됩니다!"); // "출력됩니다!"
    
    const username = "" || "Guest"; 
    console.log(username); // "Guest" (빈 문자열은 falsy 값)
    ```

---

## 3. `&&` 연산자의 단축 평가를 React에서 어떻게 활용할 수 있나요?  

- 정답  
    - `&&` 연산자는 **앞의 조건이 truthy일 때만 뒤의 표현식을 실행**하므로, JSX에서 특정 조건에 따라 컴포넌트를 렌더링할 때 자주 사용됨  
    - 조건부 렌더링에서 `if` 문 대신 간결한 코드 작성을 가능하게 함  

- 예제  
    ```jsx
    function WelcomeMessage({ isLoggedIn }) {
        return (
            <div>
                <h1>환영합니다!</h1>
                {isLoggedIn && <p>로그인된 사용자입니다.</p>}
            </div>
        );
    }
    ```
    - `isLoggedIn`이 `true`일 경우 `<p>로그인된 사용자입니다.</p>`가 렌더링됨  
    - `isLoggedIn`이 `false`일 경우 `&&` 연산자의 특성상 `<p>` 태그는 렌더링되지 않음  

---

