---
layout: single
title: "[node.js] import 시 절대 경로 사용하기"
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

# Node.js에서 `import` 시 절대 경로 사용하는 방법

Node.js 프로젝트에서 모듈을 `import`할 때 경로 설정은 매우 중요하다. 일반적으로 파일 간의 관계를 나타내기 위해 상대 경로(`../../util/logger.js`)를 사용하지만, 이는 파일 구조가 복잡해질수록 유지보수가 어려워진다. 이 글에서는 Node.js에서 **절대 경로**를 사용해 모듈을 `import`하는 방법을 소개한다.

구체적으로, 내가 진행 중인 프로젝트를 예시로 들어 `package.json` 파일 설정을 통한 절대 경로 참조 방법을 설명하겠다.

## 1. 프로젝트 파일 구조와 문제점

다음과 같은 파일 구조를 가진 Node.js 프로젝트를 살펴보자.

```bash

/project-root
  ├── app.js
  ├── /util
  │     └── logger.js
  ├── /db
  └── package.json
```

일반적으로 `app.js`에서 `logger.js`를 `import`할 때는 다음과 같이 상대 경로를 사용한다.

```jsx

import { logger } from './util/logger.js';
```

파일 구조가 깊어지면 다음과 같이 복잡해질 수 있다.

```jsx

import { config } from '../../util/logger.js';
```

이러한 상대 경로 방식은 디렉터리 구조가 변경되거나 파일이 이동할 때마다 수정이 필요하다. 특히 프로젝트 규모가 커질수록 이런 문제가 더 자주 발생한다.

## 2. 절대 경로 설정: `"type": "module"`과 `"imports"`

Node.js에서는 이러한 경로 문제를 **절대 경로**로 해결할 수 있다. 이전 포스트에 있는 방법대로 `package.json` 파일에 `"type": "module"` 설정과 `"imports"` 옵션을 추가하면 된다.

### 2.1. `package.json` 설정

프로젝트 루트의 `package.json` 파일은 다음과 같다.

```json

{
  "name": "wooboapp",
  "version": "1.0.0",
  "description": "WOOBO WEB APPLICATION SYSTEM, NODE VERSION v22.11.0",
  "main": "app.js",
  "type": "module",
  "imports": {
    "#db/*": "./db/*",
    "#router/*": "./router/*",
    "#middleware/*": "./middleware/*",
    "#util/*": "./util/*",
    "#config/*": "./config/*"
  },
  "dependencies": {
    "dotenv": "^16.4.5",
    "express": "^4.21.1",
    "figlet": "^1.8.0"
  },
  "devDependencies": {
    "nodemon": "^3.1.7"
  }
}
```

여기서 핵심은 `"type": "module"`과 `"imports"` 설정이다.

- **`"type": "module"`**: 이 설정으로 ES 모듈을 사용할 수 있어 `import`와 `export` 구문을 활용할 수 있다.
- **`"imports"`**: 이 항목은 경로 별칭(path alias)을 정의한다. `#`으로 시작하는 별칭으로 절대 경로처럼 사용할 수 있다.

### 2.2. `imports` 사용 예시

이제 `app.js`에서 `logger.js` 파일을 다음과 같이 절대 경로로 가져올 수 있다.

```jsx

// app.js
import express from "express";
import { logger } from "#util/logger.js";
```

이렇게 하면 파일 위치가 바뀌어도 경로 별칭만 올바르다면 수정할 필요가 없다.

## 3. 절대 경로 사용의 이점

### 3.1. 경로 관리의 간편함

**절대 경로**를 사용하면 파일 구조가 변경되어도 참조 경로를 수정할 필요가 없다. 상대 경로(`../../util/logger.js`)와 비교하면 유지보수가 훨씬 쉽다.

### 3.2. 코드의 가독성 향상

`#util/logger.js`와 같은 명확한 절대 경로는 코드 가독성을 높인다. 복잡한 상대 경로와 달리, 절대 경로는 파일 위치를 직관적으로 보여준다.

## 4. 추가적인 절대 경로 설정 방법

### 4.1. `NODE_PATH` 설정

예전에는 환경 변수 `NODE_PATH`로 절대 경로를 설정했다. 하지만 이 방식은 운영체제별로 설정이 다르고 복잡하다. 현재는 `"imports"`와 같은 최신 방식이 권장된다.

### 4.2. `module-alias` 패키지 사용

`module-alias` NPM 패키지로도 경로 별칭을 설정할 수 있다. 하지만 Node.js 내장 기능인 `package.json`의 `"imports"`가 더 표준적이고 간편하다.

## 5. 정리

Node.js에서 **절대 경로**로 모듈을 가져오면 프로젝트의 유지보수성과 가독성이 높아진다. `"type": "module"`과 `"imports"` 옵션으로 브라우저와 동일한 방식의 모듈 관리가 가능하다. 프로젝트 시작 시 경로 설정을 잘 해두면 개발이 훨씬 수월해진다.

이제 Node.js 프로젝트에서 절대 경로를 활용해 모듈을 `import`해보자. 코드의 가독성과 유지보수성이 한층 개선될 것이다.