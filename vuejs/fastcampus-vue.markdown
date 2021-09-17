---
layout: page
title: "패캠정리: Vue"
---

<div class="alert alert-secondary" role="alert">
  <h4>Vue</h4>
  <p>
    [패스터캠퍼스] 한 번에 끝내는 Node.js 웹 프로그래밍 초격차 패키지 Online<br>
    - 3. 프론트엔드 part1, CH05 부터
  </p>
</div>

#### #. 관련 링크

- [한글 Vue.js](https://kr.vuejs.org/)
- [한글 Vue.js 3](https://v3.ko.vuejs.org/)
- [Vue.js](https://vuejs.org/)
- [Vue CLI](https://cli.vuejs.org/)

<br>

---

### 🍱 실행환경: Vue CLI

<div class="alert alert-danger" role="alert">
  <h4>🍎 회사 폐쇄망(proxy)</h4>
  <p>
    <em><strong>stack overflow</strong>: <a href="https://stackoverflow.com/questions/34498736/npm-self-signed-cert-in-chain" class="alert-danger">NPM self_signed_cert_in_chain</a></em>
  </p>
  <p>
    <strong>방법#1</strong><br>
      <code>$ npm config set registry="http://registry.npmjs.org/"</code><br>
    <strong>방법#2</strong> (비추)<br>
      <code>$ npm config set strict-ssl false</code>
  </p>
</div>

<br>
#### #. 확인(@vue/cli)

```
  $ npm ls --depth=0 -g
  # 또는
  $ yarn global list

  $ vue --version
  @vue/cli 4.2.3
```

<br>
#### #. 설치

```
  $ npm install -g @vue/cli
  # 또는
  $ yarn global add @vue/cli
```

#### #. 업그레이드

```
  $ npm update -g @vue/cli
  # 또는
  $ yarn global upgrade --latest @vue/cli

  $ vue --version
  @vue/cli 4.5.13
```

<br>
#### #. hello world

```
  $ vue create hello-world

  # 일단 Vue 2버전으로 한다. `Default ([Vue 2] babel, eslint)` 선택
  # 현재 @vue/cli를 npm으로 설치했기에 `Use NPM` 선택
  # 설치 완료 후

  $ cd hello-world
```

<div class="alert alert-info" role="alert">
  <h4>@vue/cli config:</h4>
  <p>
    처음 실행할 때, <strong>패키지 관리자</strong>를 선택하는 단계가 나온다.<br>
    <em>(이후에는 config에 저장되어 묻지 않는다)</em><br>
    <strong>@vue/cli</strong>를 <strong>npm으로 설치</strong>했기에 <code>Use NPM</code>으로 선택했지만,
    <code>Yarn</code>으로 변경해보자.<br>
    <p>
      <em>
      $ vue config<br>
      # 설정된 정보와 함께 관리하는 ".vuerc" 파일의 경로가 나온다.<br>
      <br>
      $ vi .vuerc<br>
      # 관련 항목은 "packageManager"이다.<br>
      </em>
    </p>
  </p>
</div>

<br>
#### #. 추가 도구

- 크롬 확장 프로그램: **_Vue.js devtools_**
- VSCode 확장
  - **_vue_**: Syntax Highlight for Vue.js
  - **_Vue 3 Snippets_**: A Vue.js 3 And Vue.js 2 Code Snippets Extension

<br>

---

### 👉 작성하기

VSCode 확장(Vue 3 Snippets)으로<br>
편집기에서 `'vuein'`를 치고 **Tab 키** 또는 **Enter 키**를 누르면 기본 구조가 나온다.

---

#### 선언적 렌더링 > 컴포넌트 시스템 > 대규모 어플리케이션 상태관리 > 빌드 시스템 > 데이터 퍼시스턴시

위 타이틀이 왜 나왔는지 몰라서 그냥 둠.
추후 필요없으면 삭제

<br>

---
