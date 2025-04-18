## 1. URI를 어떻게 인코딩 할 수 있을까요?

- 정답 : 
  - JavaScript에서 URI를 인코딩하는 방법은 encodeURI()와 encodeURIComponent() 함수를 사용하는 것입니다.
  - encodeURI(): 전체 URI에서 예약된 문자를 제외하고 인코딩합니다.
  - encodeURIComponent(): 모든 문자를 인코딩하여 개별 구성 요소를 안전하게 다룰 수 있도록 합니다.


---

## 2. 호이스팅이 왜 일어날까요?

- 정답 : 
  - 호이스팅은 JavaScript 엔진이 코드를 실행하기 전에 변수와 함수 선언을 메모리에 먼저 등록하는 과정에서 발생합니다.
  - 이는 실행 컨텍스트생성 시 환경 레코드에 변수와 함수가 미리 저장되기 때문입니다.

  ### 2-1 '이는 실행 컨텍스트생성 시 환경 레코드에 변수와 함수가 미리 저장되기 때문입니다.' 이 말이 무슨 말인가요?

  - 정답 : 
    - JavaScript 코드가 실행되기 전, 실행 컨텍스트가 생성됩니다.
    - 이때 환경 레코드라는 곳에 변수와 함수의 선언 정보가 먼저 저장되는데,
    - 이 과정에서 호이스팅이 발생합니다.

    - 즉, 코드를 실행하기 전에 변수와 함수가 메모리에 등록되기 때문에
    - 코드의 실제 작성 위치와 상관없이 먼저 선언된 것처럼 동작하는 것입니다.

