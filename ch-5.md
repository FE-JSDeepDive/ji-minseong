# Chapter-5 표현식과 문

---

## 0x~, 0o~

- **octal"**(옥탈)은 8진수를 의미하며, 8진수 표기를 위해 `0o`가 사용됨.
    
    ```jsx
    console.log(0o10); // 8 (8진수 10 = 10₈ = 8₁₀)
    console.log(0o77); // 63 (7×8 + 7 = 63₁₀)
    ```
    
- **"hexadecimal"**(헥사데시멀)의 **"x"**를 따서  16진수 표기를 위해`0x`가 사용됨.
    
    ```jsx
    console.log(0x10); // 16 (16진수 10 = 16₁₀)
    console.log(0xFF); // 255 (16×15 + 15 = 255₁₀)
    ```
    
- ES5 방식 (혼란의 원인)
    
    ES6(ECMAScript 2015) 이전에는 **8진수 표기가 `0`(숫자 0)으로 시작**했음. 하지만 이 방식이 **혼란을 유발**했기 때문에, ES6에서 `0o`를 공식적으로 도입
    
    ```jsx
    console.log(010); // 8 (8진수 10 → 10₈ = 8₁₀)
    console.log(08);  // 8 (8진수로 해석되지 않고 10진수)
    console.log(09);  // 9 (8진수로 해석되지 않고 10진수)
    ```
    
    ⇒ 010은 8진수로 해석됨 (8₁₀)
    ⇒ 08이나 09는 10진수로 해석됨 (혼란 발생)
    
    ```jsx
    console.log(0o10); // 8
    console.log(0o8);  // SyntaxError (8진수는 0~7까지만 허용)
    console.log(0x10); // 16
    ```
    
    | 8진수 값 | 10진수 변환 |
    | --- | --- |
    | 0o1 | 1 |
    | 0o2 | 2 |
    | 0o7 | 7 |
    | 0o10 | 1 × 8 + 0 = 8 |
    | 0o11 | 1 × 8 + 1 = 9 |
    | 0o12 | 1 × 8 + 2 = 10 |
    | 0o20 | 2 × 8 + 0 = 16 |

---

## ESLint 동작 방식

“ESLint는 구성 가능한 JavaScript linter입니다. JavaScript 코드에서 문제를 찾고 수정하는 데 도움이 됩니다. 문제는 잠재적인 런타임 버그부터 모범 사례를 따르지 않는 것, 스타일 문제까지 다양합니다.”

ES는 Ecma Script를 의미, Lint는 소스 코드를 분석하여 프로그램 오류, 버그, 스타일 오류, 의심스러운 구조체에 표시(flag)를 달아놓기 위한 도구를 의미

(출처 : https://eslint.org/docs/latest/contribute/architecture/)
![img](https://eslint.org/docs/latest/assets/images/architecture/dependency.svg)

**실행 및 진입점**

- **`bin/eslint.js`** → **명령줄(CLI) 실행 파일**
- **`lib/api.js`** → `require("eslint")`의 **진입점 (Entry Point)**, `Linter`, `ESLint`, `RuleTester`, `SourceCode` 등 주요 객체를 노출

**CLI 관련**

- **`lib/cli.js`** → **ESLint CLI의 핵심**, 명령어 실행, 파일 읽기, 디렉터리 탐색 및 출력 처리
- **`lib/cli-engine/`** → `CLIEngine`을 사용해 **구성 파일, 파서, 플러그인, 포매터 로딩 및 코드 검증** 수행

**코드 검증 및 분석**

- **`lib/linter/`** → ESLint의 **핵심 코드 검증 클래스**, 직접 JavaScript 코드 검증 (파일 I/O 없음)
- **`lib/source-code/`** → **파싱된 소스 코드(AST) 관리 클래스**, 코드와 AST(추상 구문 트리) 다룸

**규칙 및 테스트**

- **`lib/rules/`** → **내장 ESLint 규칙 저장소**
- **`lib/rule-tester/`** → Mocha 기반 **테스트 유틸리티**, ESLint 규칙의 단위 테스트 지원

과정

- **CLI 실행 (`bin/eslint.js`) → API 처리 (`lib/api.js`) → 코드 검증 (`lib/linter/`) → 결과 출력 (`lib/cli.js`)**
- **`lib/rules/`에 기본 규칙 저장, `lib/rule-tester/`로 테스트 가능**