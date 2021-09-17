---
layout: page
title: "05. Class와 Style 바인딩"
date: 2021-09-09 09:00:00 +0900
---

##### 관련 URL

- [클래스와 스타일 바인딩](https://kr.vuejs.org/v2/guide/class-and-style.html), [Class and Style Bindings](https://vuejs.org/v2/guide/class-and-style.html)

<br>

---

데이터 바인딩에 대한 일반적인 요구는 엘리먼트의 class 목록과 인라인 스타일을 조작하는 것이다.
둘 다 속성이므로 `v-bind`를 사용하여 처리할 수 있다. 표현식으로 최종 문자열만 계산하면 된다.
그러나 문자열 연결을 간섭하는 것은 성가시고 오류가 발생하기 쉽다.\
이러한 이유로 Vue는 `v-bind`가 `class` 및 `style`과 함께 사용될 때 특별한 개선 사항을 제공한다.
문자열 외에도 표현식은 개체 또는 배열로 평가될 수도 있습니다.
