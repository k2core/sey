---
layout: page
title: "01. 시작하기"
date: 2021-08-23 09:00:00 +0900
background: "/assets/img/vuejs/1.jpg"
---

**Vue 공식 가이드**를 참고하여 순서대로 정리한다.\
꼭 필요로 한 것들만 기록한다. 필요시 가이드를 정독하자.\
버전 3이 나와 있지만, **일단 버전 2로 한다.**

##### 관련 URL

- [시작하기](https://kr.vuejs.org/v2/guide/), [Introduction](https://vuejs.org/v2/guide/index.html)

<br>

---

Vue의 이해를 돕기 위해 가이드에 나온 소스 몇 개를 살펴보자.

#### CDN

- development 버전:

```
  <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
```

- production 버전:

```
  <script src="https://cdn.jsdelivr.net/npm/vue@2"></script>
```

🥕 Vue를 시험해 볼 수 있는 가장 쉬운 방법: [JSFiddle Hello World 예제](https://jsfiddle.net/chrisvfritz/50wL7mdz/)

<br>

<div class="alert alert-primary" role="alert">
  🥗 아래 내용의 소스는 <a class="alert-primary" href="./vue01-ex01.html">"여기를 클릭"</a>
</div>

<br>

#### 소스#1> 선언적 렌더링(Declarative Rendering): 데이터와 DOM 연결

간단한 **템플릿** 구문을 사용하여 **DOM에서 데이터를 선언적으로 렌더링**한다.\
템플릿에 대한 부분은 아래를 참고하자.

\*. 템플릿(template) 시스템들: **[Mustache](https://mustache.github.io/)**, [Handlebars](https://handlebarsjs.com/), [Liquid(Jekyll에서 사용)](https://shopify.github.io/liquid/)<br>
\*. Web template system [(WIKIPEDIA)](https://en.wikipedia.org/wiki/Web_template_system)

<br>

```
# HTML
<div id="app">
  {{ "{{ message " }}}}
</div>

# JS
var app = new Vue({
  el: '#app',
  data: {
    message: '안녀하세요 Vue!'
  }
})
```

HTML에서 *"{{ "{{ 변수 " }}}}"*라고 쓰면, Vue 인스턴스의 `data` 속성에 정의한 변수와 바인딩 된다.

소스를 실행하고, 개발자 도구 콘솔에서 `app.message`를 변경해보자.\
**Vue 인스턴스**의 이미 정의된 속성들에는 `$`가 붙는다:\
 예) `el` -> `$el`, `data` -> `$data`\
Vue 인스턴스의 `data` 속성에 선언한 **변수**는 다음과 같이 접근 가능하다:<br>
예) `app.변수명`, 위 속성의 경로를 대입하면 `app.$data.변수명`도 가능하다.

<br>

#### 소스#02> 선언적 렌더링: 엘리먼트 속성(title)에 bind

`v-bind:title="변수"`는 엘리먼트의 'title' 속성과 바인딩 된다.

`v-bind` 속성은 **디렉티브**라고 한다.

<div class="alert alert-warning" role="alert">
  <h4>interpolation:</h4>
  써넣음, 써넣은 어구, 보간법(補間法), 내삽법(內揷法)<br>
  'interpolotion(보간법)'이라는 워딩이 여러 곳에서 나온다. 문화가 궁금하다.
</div>

<br>

#### 소스#03: 조건문

`v-if="변수"`

`v-if`와 `v-show`의 차이점: if는 렌더링 자체가 되고/안되고, show는 스타일 속성인 display로 화면에 표시하고/안하고

<br>

#### 소스#04: 반복문

`v-for="반복변수 in 변수"`

<br>

#### 소스#05: 사용자 입력 핸들링: 이벤트 리스너

`v-on` **디렉티브**를 사용하여 Vue 인스턴스에서 메소드를 호출하는 이벤트 리스너를 추가 할 수 있다

`v-on:click="메소드"`

<br>

#### 소스#06: 사용자 입력 핸들링: 양방향 바인딩(v-model)

Vue는 또한 양식에 대한 입력과 앱 상태를 양방향으로 바인딩하는 `v-model` **디렉티브**를 제공한다.

<br>

---

#### 컴포넌트를 사용한 작성방법

컴포넌트 시스템은 Vue의 또 다른 중요한 개념입니다.
이는 작고 독립적이며 재사용할 수 있는 컴포넌트로 구성된 대규모 애플리케이션을 구축할 수 있게 해주는 추상적 개념입니다.
생각해보면 거의 모든 유형의 애플리케이션 인터페이스를 컴포넌트 트리로 추상화할 수 있습니다.

`Vue.component("컴포넌트명", {})` 사용

_소스#07 참조_

*'소스#07'*은 인위적으로 만든 예시이지만, 우리는 앱을 두 개의 더 작은 단위로 분리할 수 있었고,
자식을 props 인터페이스를 통하여 부모로부터 합리적인 수준으로 분리할 수 있었습니다.
이제 앞으로는 부모 앱에 영향을 주지 않으면서 `<todo-item>` 컴포넌트를 더 복잡한 템플릿과 로직으로 더욱 향상시킬 수 있을 것입니다.

대규모 애플리케이션에서는 개발을 보다 쉽게 관리 할 수 있도록 전체 앱을 컴포넌트로 나누는 것이 필수적입니다.

##### #. 커스텀 엘리먼트와의 관계

Vue 컴포넌트는 [Web Components Spec](https://www.w3.org/wiki/WebComponents/)의 일부인
커스텀 엘리먼트와 매우 유사하다는 것을 눈치 챘을 수 있습니다.
Vue의 컴포넌트 구문은 스펙에 따라 느슨하게 모델링 되었기 때문입니다.
예를 들어 Vue 컴포넌트는
[Slot API](https://github.com/w3c/webcomponents/blob/gh-pages/proposals/Slots-Proposal.md)와
`is` 특수 속성을 구현합니다. 그러나 몇 가지 중요한 차이가 있습니다:

1. Web Components Spec은 최종안이 정해졌지만 모든 브라우저들이 기본적으로 구현되는 것은 아닙니다.
   현재 사파리 10.1+, 크롬 54+ 그리고 파이어폭스 63+ 기본적으로 Web Components를 지원합니다.
   이에 비해 Vue 컴포넌트는 지원되는 모든 브라우저 (IE 9 이상)에서 폴리필을 필요로 하지 않으며 일관된 방식으로 작동합니다.
   필요한 경우 Vue 컴포넌트는 기본 커스텀 엘리먼트 내에 래핑할 수 있습니다.

2. Vue 컴포넌트는 컴포넌트간 데이터의 흐름을 비롯해, 커스텀 이벤트와 통신,
   빌드 도구와의 통합 등 네이티브 커스텀 엘리먼트에서 사용할 수 없었던 중요한 기능을 제공합니다.

Vue는 내부적으로 커스텀 엘리먼트를 사용하지 않지만, 커스텀 엘리먼트로 사용 또는 배포하는 경우에는
[뛰어난 상호운용성](https://custom-elements-everywhere.com/#vue)을 가집니다.
Vue CLI는 자기자신을 네이티브 커스텀 엘리먼트로서 등록하는 Vue 컴포넌트의 빌드도 지원하고 있습니다.
