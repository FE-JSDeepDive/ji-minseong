## 1. const로 선언된 객체의 값을 변경할 수 있을까요? 가능하다면 어떻게 변경할 수 있을까요?

- 정답
  - 변경할 수 있습니다.
  - const 키워드로 선언된 변수는 재할당과 재선언이 금지되지만,<br/>객체가 저장된 변수에는 객체의 참조 값이 저장되기 때문에 객체의 속성(프로퍼티)은 변경할 수 있습니다.

---

## 2.아래 코드의 결과값을 말씀해주세요.

```javascript
{
  console.log(a); // ?
  let a = 10;
  console.log(a); // ?
}

{
  var b = 20;
  console.log(b); // ?
}
console.log(b); // ?
```

- 정답 : ReferenceError 발생 (TDZ), 10, 20, 20

  - 첫 번째 블록 {}

    - console.log(a); → let a는 호이스팅되지만 TDZ(Temporal Dead Zone)에 걸려 ReferenceError 발생
    - let a = 10; 선언 후
    - console.log(a); → 10 출력

  - 두 번째 블록 {}

    - var b = 20; 실행 → 전역 변수로 선언됨 (블록 스코프 영향을 받지 않음)
    - console.log(b); → 20 출력
    - 블록 바깥 console.log(b);

    - b는 var로 선언되었으므로 함수 레벨 스코프 → 전역 변수로 접근 가능
    - console.log(b); → 20 출력
