---
title: "npm init"
excerpt: "npm init을 하여 nodejs package를 만들자"
categories:
  - node.js
tags: 
  - node.js
  - npm
toc_label: "npm init"
toc: true
date: 2024-11-22
last_modified_at: 2024-11-22
---

`npm init`은 Node.js 프로젝트를 시작할 때 반드시 거쳐가는 첫 번째 단계로, 프로젝트의 뼈대를 만드는 역할을 한다. 이 명령어는 단순한 실행 하나로 개발의 시작을 정리하고, 관리의 기반이 되는 `package.json`이라는 중요한 파일을 생성한다.

---

### `npm init`의 기본 개념

`npm init` 명령은 프로젝트의 메타데이터를 설정하는 작업으로 시작된다. 이 과정에서 프로젝트의 이름, 버전, 설명, 메인 파일, 테스트 명령어, 저장소 URL, 키워드, 작성자, 라이선스와 같은 기본적인 정보들을 입력받는다. 모든 질문에 답하고 나면 `package.json`이라는 JSON 형식의 파일이 생성되며, 이 파일은 이후 프로젝트의 의존성 관리와 스크립트 실행의 중심축 역할을 한다.

---

### `npm init`의 사용법

### 1. 기본 실행

```bash

npm init

```

`npm init` 명령어를 실행하면 단계별로 질문이 나타난다. 여기서 입력하는 값들은 차후 프로젝트의 정보를 정리하는 데 사용된다.

예를 들어, 실행 후 나타나는 질문들은 다음과 같다.

1. **package name**: 프로젝트의 이름. 기본값으로 현재 디렉토리 이름이 제안된다.
2. **version**: 프로젝트의 초기 버전. 기본값은 `1.0.0`.
3. **description**: 프로젝트의 간단한 설명.
4. **entry point**: 진입 파일. 기본값은 `index.js`.
5. **test command**: 테스트를 실행하기 위한 명령어.
6. **git repository**: 프로젝트가 연결될 Git 저장소 URL.
7. **keywords**: 프로젝트와 관련된 키워드. 배열 형태로 입력 가능.
8. **author**: 작성자의 이름.
9. **license**: 프로젝트의 라이선스. 기본값은 `ISC`.

입력 과정을 거치면 결과적으로 `package.json` 파일이 생성된다.

---

### 2. 빠른 초기화

```bash

npm init -y

```

시간을 절약하고 싶다면 `-y` 플래그를 붙여 기본값으로 초기화할 수 있다. 이 명령어는 모든 질문을 생략하고 자동으로 `package.json` 파일을 생성한다. 기본값으로 설정된 내용은 다음과 같다.

```json

{
  "name": "current-directory",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}

```

---

### `package.json` 파일의 역할

Node.js 프로젝트에서 `package.json`은 프로젝트의 모든 것을 기록하는 **중심 문서**이다. 이 파일은 다음과 같은 내용을 포함한다.

1. **프로젝트 정보**: 이름, 버전, 설명, 메인 파일, 작성자 등.
2. **의존성 관리**:
  - `dependencies`: 프로젝트 실행에 반드시 필요한 패키지.
  - `devDependencies`: 개발 중에만 필요한 패키지.
3. **스크립트 관리**:
  - `start`, `test`와 같은 명령어를 정의하여 간편하게 실행할 수 있게 한다.

---

### `npm init`과 개발 흐름의 연관성

### 1. 새로운 프로젝트의 출발점

`npm init`은 단순히 파일을 생성하는 것을 넘어, 프로젝트의 시작을 알리는 신호와도 같다. 정리된 `package.json`은 프로젝트 구성원들과의 협업이나 자동화된 배포 파이프라인에서 핵심적인 역할을 수행한다.

### 2. 의존성 추가

`npm init`으로 생성된 `package.json`에 의존성을 추가하면, 프로젝트는 더 체계적으로 관리된다. 이를 통해 실행 환경에 필요한 라이브러리와 개발 도구를 명확히 구분할 수 있다.

```bash

npm install lodash
npm install jest --save-dev

```

- `lodash`는 `dependencies`에 기록되어 실행 시 사용된다.
- `jest`는 `devDependencies`에 기록되어 개발 환경에서만 사용된다.

---

### `npm init`의 의의

`npm init`은 단순한 명령 이상의 의미를 가진다. 이는 프로젝트의 출발점이자, 모든 설정의 근간을 이루는 작업이다. 명확히 기록된 `package.json`은 협업의 기준이 되고, 프로젝트를 발전시키는 데 있어 기반을 다지는 첫걸음이라 할 수 있다.

---

### 마무리하며

`npm init`은 단순히 파일을 만드는 작업으로 끝나지 않는다. 이는 프로젝트를 조직화하고, 추후 발생할 문제를 예방하며, 협업의 표준을 제공하는 중요한 단계다. 이 명령어를 통해 생성된 `package.json`은 프로젝트의 얼굴과 같은 존재로, 이후의 모든 개발 과정을 견고하게 뒷받침한다.
