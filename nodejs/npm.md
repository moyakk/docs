Node Package Manger

## npm

설치된 버전 확인

```
npm -v
```

최신 버전으로 업그레이드
```
sudo npm install -g npm
```

## npm init

몇 가지 질문과 함께 현재 폴더에 package.json 파일을 생성한다.

```js
// package.json
{
  "name": "test",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```

- 질문에 별도의 선택을 하지 않고 엔터만 눌러서 기본값으로 생성된 package.json 파일
- name 의 경우 현재 폴더명이 기본값으로 사용되는 것 같다.

```js
// package.json
{
  "name": "vuejs",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "bootstrap": "^4.6.0"
  }
}
```

- 프로젝트에 필요한 패키지는 dependencies 항목에서 관리된다.
  - npm v5 이상에서는 npm install 시 자동으로 등록되나, 이하 버전에서는 `--save` 옵션을 줘야 한다.
  - package.json 이 있는 폴더에서 `npm install` 만 하면 depencencies 항목에 있는 모든 패키지가 자동으로 설치된다.

## npm install
> npm install 또는 npm i

자주 사용되는 옵션들

- `-g` 또는 `--global`
  - 패키지를 어디에서나 사용 할 수 있도록 전역(global) 모드로 설치한다.
    - 해당 옵션을 적용하지 않으면 현재 작업폴더에 설치된다.
  - 모든 패키지는 node_modules 라는 폴더에 설치되는데, 전역 모드의 패키지 설치 경로는 아래와 같다.
    - Unix : `/usr/local/bin/node` or `/usr/local/lib/node_modules`
    - Windows 7, 10 : `%USERPROFILE%\AppData\Roaming\npm\node_modules`

## npm info
> npm info 또는 npm v, npm show

패키지 상세 정보를 출력한다.

```console
npm info bootstrap
```

## 심화학습!

### 특정 버전의 패키지가 필요한 경우
- 패키지는 편의상 bootstrap 이라고 가정한다.

패키지가 존재하는지 검색해본다.

```console
npm search bootstrap
```

패키지에서 지원하는 모든 버전의 목록을 확인한다.

```console
npm info bootstrap versions
```

패키지의 특정 버전을 설치한다.

```console
npm install bootstrap@4.6.0
```
