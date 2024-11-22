---
layout: single
title: "[node.js] nodejs의 CommonJS와 ES Module에 관하여..(feat. import 사용하기)"
excerpt: ""
categories:
  - node.js
tags: 
  - node.js
  - npm
toc_label: "nodejs"
toc: true
date: 2024-11-22
last_modified_at: 2024-11-22
---

Node.js 개발 중 `require` 를 사용하지 않고 `import` 를 사용하고 싶어서 찾아보았다.

Node.js에서는 기본적으로 `CommonJS` 모듈 시스템(`require`)을 사용하지만, ES 모듈(`import/export`)을 지원하기 위한 방법도 제공하고 있다. `package.json`에서 `"type": "module"`을 설정하면 ES 모듈을 사용할 수 있다.

---

## 1. 기본 개념: CommonJS vs ES Module

### CommonJS (기본 모듈 시스템)

- Node.js의 기본 모듈 시스템.
- `require`와 `module.exports`를 사용.
- 주요 특징:
  - 동기적으로 모듈을 로드.
  - Node.js에서 오랫동안 사용된 방식.

### 예:

```jsx

// CommonJS 방식
const fs = require('fs'); // 모듈 가져오기
module.exports = { myFunction }; // 모듈 내보내기

```

---

### ES Module (ECMAScript 모듈 시스템)

- ES6부터 도입된 표준 모듈 시스템.
- `import`와 `export` 키워드를 사용.
- 주요 특징:
  - 비동기적으로 모듈을 로드.
  - 표준화된 방식으로 브라우저와 Node.js에서 모두 사용 가능.

### 예:

```jsx

// ES Module 방식
import fs from 'fs'; // 모듈 가져오기
export const myFunction = () => {}; // 모듈 내보내기

```

---

## 2. Node.js에서 ES 모듈 사용 설정

Node.js는 기본적으로 ES 모듈을 지원하지 않지만, `package.json`에서 `"type": "module"`을 설정하면 ES 모듈을 사용할 수 있다.

### 설정 방법

1. **`package.json`에 `"type": "module"` 추가**

    ```json
    
    {
      "name": "my-project",
      "version": "1.0.0",
      "type": "module"
    }
    
    ```

  - 이 설정을 추가하면, 해당 프로젝트의 모든 `.js` 파일이 ES 모듈로 동작한다.
  - 이제 `import`와 `export`를 사용할 수 있다.
2. **파일 확장자 주의**
  - ES 모듈을 사용할 때는 `.js` 파일이어도 자동으로 ES 모듈로 인식된다.
  - CommonJS 모듈을 사용하려면 파일 확장자를 `.cjs`로 지정해야 한다.

---

### ES 모듈 사용 예시

### 1. 모듈 가져오기

```jsx

// math.js
export const add = (a, b) => a + b;

// index.js
import { add } from './math.js';
console.log(add(2, 3)); // 5

```

### 2. 모듈 내보내기

```jsx

// utils.js
export function sayHello(name) {
  return `Hello, ${name}!`;
}

// app.js
import { sayHello } from './utils.js';
console.log(sayHello('Austin')); // Hello, Austin!

```

---

## 3. CommonJS와 ES Module의 혼합 사용

### CommonJS에서 ES 모듈 가져오기

- CommonJS(`require`)로 ES 모듈을 가져올 때는 동작이 약간 다르다.

```jsx

// app.cjs
const math = require('./math.js'); // ES 모듈은 default export로만 가져올 수 있음
console.log(math.add(2, 3)); // undefined

```

### ES 모듈에서 CommonJS 가져오기

- ES 모듈(`import`)로 CommonJS를 가져올 때는 기본적으로 전체 객체를 가져온다.

```jsx

// app.js
import fs from 'fs';
console.log(fs.readFileSync('./file.txt', 'utf8'));

```

---

## 4. `type: "module"` 사용 시 주의사항

### 1. `require`를 사용할 수 없다

- `"type": "module"` 설정 시, `require`는 기본적으로 사용할 수 없다.
- CommonJS 모듈을 사용하려면 `import`를 사용하거나, Node.js의 `createRequire`를 활용해야 한다.

```jsx

// require 사용 예
import { createRequire } from 'module';
const require = createRequire(import.meta.url);
const fs = require('fs');
console.log(fs.readFileSync('./file.txt', 'utf8'));

```

---

### 2. 파일 확장자 명시

- ES 모듈에서는 **확장자를 반드시 명시**해야 한다.

    ```jsx
    
    // 올바른 방식
    import { add } from './math.js';
    
    // 오류 발생
    import { add } from './math'; // 확장자를 생략하면 안 됨
    
    ```


---

### 3. `import.meta.url`

- ES 모듈에서는 `__dirname`과 `__filename`이 존재하지 않는다.
- 대신, `import.meta.url`을 사용해 현재 모듈의 URL을 가져올 수 있다.

```jsx

console.log(import.meta.url); // 파일의 URL 출력

```

---

### 4. 호환성 문제

- 일부 오래된 패키지는 ES 모듈을 지원하지 않을 수 있다.
- 이 경우 `CommonJS` 방식으로 패키지를 사용하거나 다른 대안을 찾아야 한다.

---

## 5. ES 모듈과 CommonJS 비교 요약

| 특징 | CommonJS (`require`) | ES Module (`import/export`) |
| --- | --- | --- |
| 기본 지원 | Node.js 기본 지원 | `type: "module"` 필요 |
| 동작 방식 | 동기적 로딩 | 비동기적 로딩 |
| 키워드 | `require`, `module.exports` | `import`, `export` |
| 파일 확장자 | `.js` 기본 | `.js`, `.mjs`, `.cjs` |
| Node.js에서 지원 여부 | 기본 지원 | 14.x 이상에서 지원 |

---

## 6. 마무리

Node.js에서 `"type": "module"` 설정은 ES 모듈을 사용하는 현대적인 방식을 도입하기 위한 필수적인 단계이다. 이 설정을 통해 브라우저와 동일한 방식으로 모듈을 관리할 수 있지만, CommonJS와의 호환성 문제를 이해하고 적절히 대응해야 한다.

추가적으로, ES 모듈과 CommonJS의 혼합 환경에서 작업할 때는 확장자와 사용 방식에 주의를 기울여야 한다. 필요하다면, `createRequire`를 사용하여 두 시스템 간의 호환성을 유지할 수 있다.