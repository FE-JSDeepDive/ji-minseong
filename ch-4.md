# Chapter-4 변수

---

## 비교시 메모리 주소 주의

- 각 셀은 고유의 메모리 주소를 갖는다 => 등호 비교시 달라질 수 있음
(예시)
    - `console.log([10,20] === [10,20])` 이 예시에서 메모리 비교를 하기 때문에
    - `false`가 콘솔에 찍히게 됨

---

## var 지양

- var → 함수 스코프
- let,const → 블록 스코프 + TDZ(Temperal Dead Zone)
    
    ```jsx
    black; // throws `ReferenceError`
    const black = '#1b1b1b'; // -> 이 구문 전까지 black TDZ에 있다.
    
    black
    ```
    
    ⇒ 더 안전하게 코드 작성 가능
    
    ⇒ var는 여러번 정의해도 에러가 생기지  않음
    
    ```jsx
    var name = '12'
    var name = '34'
    console.log(name) // '34'
    ```
    
    ```jsx
    console.log(name); // undefined (에러 없이 실행됨)
    var name = "Alice";
    console.log(name); // "Alice"
    ```
    
    ⇒ 재할당 , 재선언이 가능하다, 현재 스코프에서 호이스팅 된다  ⇒ 위험할 수 있다. 
    
- 왜?
    
    ```jsx
    if (true) {
      var fruit = "apple";
    }
    console.log(fruit); // "apple" (블록을 빠져나와도 접근 가능)
    ```
    
    - var이 if문에서 재할당 된다면 → 전역에 영향을 끼친다.
        
        ⇒ let으로 바꾼다면 지역단위에만 영향을 미친다.
        
    
    ⇒ 기본적으로 `const`를 사용하고 **재할당이 필요한 경우에만** `let`을 사용
    

---

## 임시변수 제거

```jsx
function getElements() {
	const reuslt = {}; // 임시 변수
	
	result.title = document.querySelector('.title');
	result.text = document.querySelector('.text');
	result.value = document.querySelector('.value');

	return reuslt;
}

=>=>=>

function getElements() {
	return {
			title = document.querySelector('.title');
			text = document.querySelector('.text');
			value = document.querySelector('.value');
	};
}
```

⇒ 임시 변수(객체)가 생기는 순간 계속 접근해서 뭔가 바꾸고 싶은 유혹이 발생할 수 있음 

⇒ 함수를 10~100군데에서 사용가능하기에 이를 그냥 바로 반환하도록 바꾸는 것이 낫다? 

⇒ 수정사항 있을시에는 다른 함수를 묶어서 사용한다. (함수의 추상화)

⇒ 그 누구도 임시변수의 유혹을 받을 수 있지 않도록, 단순화해서 작성한다.

- 임시변수 제거
    - 임시 변수는 제거되어야한다 → 명령형으로 가득한 코드 , 로직
    - 어디서 어떻게 잘못되었는지 디버깅이 어렵다
    - 추가적으로 코드를 작성하고싶은 유혹에 빠지기 쉽다
- 해결책
    - 바로 반환 - 위의 예시
    - 구조 분해 할당
        
        ```jsx
        function getElements() {
        	const title = document.querySelector('.title');
        	const text = document.querySelector('.text');
        	const value = document.querySelector('.value');
        
        	return { title, text, value };
        }
        ```
        
    - 함수 나누기
        
        ```jsx
        const getElement = (selector) => document.querySelector(selector);
        
        function getElements() {
        	return {
        		title: getElement('.title'),
        		text: getElement('.text'),
        		value: getElement('.value'),
        	};
        }
        ```
        
    - 고차 함수
        
        ```jsx
        const createElementFetcher = (selectors) => 
          Object.fromEntries(selectors.map(sel => [sel.slice(1), document.querySelector(sel)]));
        
        const getElements = () => createElementFetcher([".title", ".text", ".value"]);
        
        ```
        
    - 선언형 코드
        
        (참고)
        
        - 명령형 :
            - **어떻게(How) 요소를 가져올지 직접 명령**하는 코드
            - `result` 객체를 선언하고, 거기에 `title`, `text`, `value`를 할당하는 방식
        - 선언형
            - **무엇(What)을 반환할지만 설명** → 코드가 직관적이고 간결
            - 중간 과정 없이 **바로 결과를 반환**
            - 불필요한 상태 변경(임시 변수)이 없음