---
layout: single
title: "npm istall"
excerpt: "npm install의 기본 개념 확인"
categories:
  - node.js
tags: 
  - node.js
  - npm
toc_label: "npm install"
toc: true
date: 2024-11-22
last_modified_at: 2024-11-22
---

`npm install`은 Node.js 프로젝트에서 패키지(모듈)를 설치하고 관리하기 위한 핵심 명령어다. 이 명령어를 통해 의존성을 추가하거나, 프로젝트의 모든 의존성을 한 번에 설치할 수 있다. `npm install`은 간단해 보이지만, 다양한 옵션과 기능을 제공하며, 이를 깊이 이해하면 프로젝트 관리가 훨씬 더 수월해진다.

---

## `npm install`의 기본 개념

### 기본 동작

- `npm install` 명령어는 **Node.js 패키지를 설치**하거나, **이미 정의된 의존성을 설치**하는 데 사용된다.
- 설치된 패키지는 **`node_modules`** 디렉토리에 저장된다.
- 설치 정보는 **`package.json`** 파일에 기록되며, 이를 통해 의존성을 관리할 수 있다.

---

## `npm install`의 주요 사용법

### 1. 모든 의존성 설치

```bash

npm install

```

- *`package.json`*에 기록된 모든 `dependencies`와 `devDependencies`를 설치한다.
- 프로젝트를 처음 클론했을 때나, 새 환경에서 작업을 시작할 때 사용한다.
- 설치된 패키지는 `node_modules` 디렉토리에 저장된다.

---

### 2. 특정 패키지 설치

```bash

npm install <package-name>

```

- 특정 패키지를 설치하며, 설치된 패키지는 기본적으로 **`dependencies`*에 추가된다.

### 예:

```bash

npm install express

```

- `express`가 설치되고, **`package.json`*의 `dependencies`에 기록된다.

```json

"dependencies": {
  "express": "^4.18.2"
}

```

---

### 3. 개발용 패키지 설치

```bash

npm install <package-name> --save-dev

```

- 패키지를 **`devDependencies`*에 추가한다.
- 개발 환경에서만 필요한 도구들을 설치할 때 사용한다.

### 예:

```bash

npm install eslint --save-dev

```

- `eslint`가 설치되고, **`package.json`*의 `devDependencies`에 기록된다.

```json

"devDependencies": {
  "eslint": "^8.47.0"
}

```

---

### 4. 글로벌 패키지 설치

```bash

npm install -g <package-name>

```

- 패키지를 전역(global)으로 설치하여, 어디서든 사용할 수 있게 한다.
- 주로 CLI(Command Line Interface) 도구를 설치할 때 사용된다.

### 예:

```bash

npm install -g nodemon

```

- `nodemon`이 전역으로 설치되어, 명령어 `nodemon`을 어디서든 사용할 수 있다.

---

### 5. 특정 버전 설치

```bash

npm install <package-name>@<version>

```

- 원하는 버전의 패키지를 설치한다.
- 버전을 명시하지 않으면 기본적으로 최신 버전이 설치된다.

### 예:

```bash

npm install express@4.17.1

```

- `express`의 `4.17.1` 버전이 설치된다.

---

### 6. 패키지 제거

```bash

npm uninstall <package-name>

```

- 특정 패키지를 제거하며, `dependencies` 또는 `devDependencies`에서도 해당 패키지를 삭제한다.

### 예:

```bash

npm uninstall express

```

---

## 설치 시 중요한 플래그들

### 1. `-save-dev`

- 개발용 패키지를 설치하며, `devDependencies`에 추가한다.

### 2. `g`

- 패키지를 전역(global)으로 설치한다.

### 3. `-save-exact`

- 정확한 버전을 설치하고, 버전 앞에 `^`나 `~`를 생략한다.

### 예:

```bash

npm install lodash --save-exact

```

- `package.json`에 정확한 버전만 기록:

    ```json
    
    "dependencies": {
      "lodash": "4.17.21"
    }
    
    ```


### 4. `-force`

- 충돌이나 오류가 발생해도 강제로 설치를 진행한다.

---

## `npm install`의 내부 작동 방식

1. **`package.json` 확인**:
  - 설치할 패키지가 이미 `package.json`에 정의되어 있다면, 해당 정보를 기반으로 설치를 진행한다.
2. **`package-lock.json` 사용**:
  - 정확한 버전 관리를 위해 **`package-lock.json`** 파일을 확인하고, 동일한 의존성 구조를 유지하며 설치한다.
3. **패키지 다운로드**:
  - 패키지를 `node_modules` 디렉토리에 다운로드한다.
4. **캐싱**:
  - 다운로드된 패키지는 로컬 캐시에 저장되며, 이후 동일한 패키지를 설치할 때 빠르게 처리된다.

---

## 의존성 설치의 두 가지 유형

1. **dependencies**:
  - 앱이 실행될 때 반드시 필요한 패키지.
  - 배포 환경에서도 설치된다.
2. **devDependencies**:
  - 개발 중에만 필요한 패키지.
  - 테스트 도구, 코드 품질 검사 도구, 빌드 도구 등이 여기에 해당된다.

---

## 실무에서의 사용 사례

1. **새 프로젝트 시작**:
  - `npm init`으로 프로젝트를 초기화하고, `npm install`로 필요한 라이브러리를 추가.
2. **협업 시**:
  - 깃허브에서 프로젝트를 클론한 후, `npm install`을 실행하여 의존성을 설치.
3. **버전 충돌 해결**:
  - 정확한 버전을 지정하여 설치하거나, `-save-exact` 옵션을 사용하여 일관성 유지.
4. **테스트 환경 구성**:
  - 테스트 및 개발 도구를 `-save-dev` 옵션으로 설치하여 환경을 깔끔하게 분리.

---

## npm install 과 npm install —save 차이

### 1. **`npm install packagename`**

- **설명**: 해당 명령어는 패키지를 **`node_modules`** 디렉토리에 설치하고, `package.json` 파일에 아무런 영향을 미치지 않음.
- **주요 특징**:
  - 패키지가 설치될 뿐, `dependencies`나 `devDependencies`에 추가되지 않음.
  - `package.json` 없이도 설치 가능.
  - 주로 임시적으로 사용하는 경우에 적합 (프로젝트에서 영구적으로 관리하지 않을 경우).

---

### 2. **`npm install packagename --save`**

- **설명**: 패키지를 **`node_modules`** 디렉토리에 설치하면서, 동시에 `package.json`의 **`dependencies`** 항목에 추가.
- **주요 특징**:
  - `package.json` 파일의 **`dependencies`** 섹션에 설치된 패키지가 기록됨.
  - 기록된 패키지는 `npm install`을 실행할 때 자동으로 설치됨.
  - Node.js 앱 실행에 필요한 패키지를 관리하는데 적합.

---

### 3. **현재는 `-save`가 불필요하다**

- **변경사항**: `npm` 5.0 이상부터는 **`-save` 옵션이 기본값**으로 설정됨.
  - 즉, **`npm install packagename`** 만 입력해도 자동으로 `package.json`의 `dependencies`에 추가됨.
- **결론**: **`npm install packagename --save`*를 별도로 입력할 필요가 없음.

---

### 4. 무엇이 더 좋은가?

- **현재 관점에서 더 나은 명령어**:
  - 그냥 **`npm install packagename`*를 사용하면 충분함.
  - `-save`를 명시적으로 적을 필요가 없어졌기 때문.
- **특별한 경우**:
  - 개발용 패키지로 설치하고 싶다면 **`-save-dev`** 옵션을 사용해야 함.

      ```bash
      
      npm install packagename --save-dev
      
      ```

  - 이는 `package.json`의 **`devDependencies`*에 추가됨.

---

### 결론

- **npm 5.0 이상**: 그냥 `npm install packagename`를 사용하자.
- **개발용 패키지**: `npm install packagename --save-dev`를 사용하자.
- `-save`는 옛날 방식이므로 굳이 사용할 필요가 없음.

---

## 그냥 install과 —save-dev 개발용 패키지 차이

### 1. **`dependencies`와 `devDependencies`의 차이**

- **`dependencies`**:
  - 프로젝트를 **실제 실행**할 때 필요한 패키지들이 저장됨.
  - 서버에서 실행하거나 배포 환경에서 반드시 필요한 라이브러리.
  - 예:
    - 웹 서버를 실행하기 위해 필요한 `express`
    - 데이터베이스와 연결하기 위한 `mongoose` 같은 라이브러리.
  - `package.json`에 추가되는 위치:

      ```json
      
      "dependencies": {
        "express": "^4.18.2"
      }
      
      ```

- **`devDependencies`**:
  - **개발 중에만** 필요한 패키지들이 저장됨.
  - 배포 후 애플리케이션 실행에는 필요하지 않음.
  - 예:
    - 코드 품질을 확인하는 `eslint`
    - 테스트 도구 `jest`
    - 빌드 툴 `webpack` 등.
  - `package.json`에 추가되는 위치:

      ```json
      
      "devDependencies": {
        "eslint": "^8.47.0"
      }
      
      ```


---

### 2. **`npm install`의 작동 방식에 따른 차이**

- **`npm install` 실행 시**:
  - `dependencies`와 `devDependencies`에 있는 모든 패키지가 설치됨.
- **`NODE_ENV=production npm install` 실행 시**:
  - **`devDependencies`는 설치되지 않음.**
  - 이는 배포 환경에서 개발용 패키지를 불필요하게 포함하지 않도록 하기 위함.

---

### 3. **언제 `-save-dev`를 사용할까?**

- **`-save-dev`가 적합한 경우**:
  - 애플리케이션이 아닌 **개발 환경**에서만 필요한 도구들:
    - 테스트 라이브러리 (e.g., `jest`, `mocha`)
    - 번들러 및 빌드 도구 (e.g., `webpack`, `vite`)
    - 코드 품질 검사 도구 (e.g., `eslint`, `prettier`)
    - 타입 체커 (e.g., `typescript`)
- **`dependencies`가 적합한 경우**:
  - 실제 앱이 실행되기 위해 반드시 필요한 패키지:
    - 웹 프레임워크 (e.g., `express`, `koa`)
    - 데이터베이스 클라이언트 (e.g., `pg`, `mongoose`)
    - 유틸리티 라이브러리 (e.g., `lodash`, `dayjs`)

---

### 4. **예시**

- `express` 설치:

    ```bash
    
    npm install express
    
    ```

  - `dependencies`에 추가.
  - 배포 시에도 포함되어야 하므로.
- `jest` 설치:

    ```bash
    
    npm install jest --save-dev
    
    ```

  - `devDependencies`에 추가.
  - 테스트만 개발 중에 필요하며, 배포 후에는 필요 없으므로.

---

### 5. **왜 나눠서 관리해야 할까?**

- **최적화된 배포 환경**:
  - 개발용 패키지가 포함되지 않으면 설치 용량이 줄어들고 빌드 속도가 빨라짐.
  - 서버에서 불필요한 도구가 실행되지 않으므로 보안과 성능이 향상됨.
- **프로젝트 구조 관리**:
  - `dependencies`와 `devDependencies`를 나눔으로써 패키지의 목적과 용도를 명확히 구분 가능.

---

### 결론

- **`-save-dev`**: 개발 중에만 필요한 패키지.
- **일반 설치 (`dependencies`)**: 실행 환경에서 필요한 패키지.

`npm init`은 Node.js 프로젝트를 시작할 때 반드시 거쳐가는 첫 번째 단계로, 프로젝트의 뼈대를 만드는 역할을 한다. 이 명령어는 단순한 실행 하나로 개발의 시작을 정리하고, 관리의 기반이 되는 `package.json`이라는 중요한 파일을 생성한다.

---
---

## 마무리하며

`npm install`은 단순히 패키지를 설치하는 명령어가 아니다. 프로젝트 의존성을 효율적으로 관리하고, 협업과 배포의 일관성을 유지하는 데 있어 필수적인 도구다. 적절한 옵션과 사용법을 숙지하면, 프로젝트를 보다 체계적으로 관리할 수 있다.