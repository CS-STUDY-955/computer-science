# Component

- 컴포넌트 : 화면을 구성할 수 있는 `블록`을 의미
- 컴포넌트를 생성할 때는 `설계` 가 중요함
- 명확하게 설계되지 않는다면,
  - 전반적인 코드의 가독성과 유지관리 효율성 저하
  - 컴포넌트 구조의 복잡성 증가
  - 독립적인 컴포넌트로의 변이

## 컴포넌트 특징

1. 화면을 빠르게 구조화하여 일괄적인 패턴으로 개발할 수 있음
2. 코드를 쉽게 이해하고 재사용 가능
3. 단위테스트에 용이

## 컴포넌트 생성 규칙

1. 의미있는 네이밍 만들기
2. 하나의 단어가 아닌 2가지 단어가 조합된 형태로 작성 권장
3. 카멜케이스

## 컴포넌트 간 통신

### props : 부모 컴포넌트가 자식 컴포넌트에게 전달하는 데이터

```html
<!--Sub.vue-->
<template>
  <div class="sub">name : {{name}}, age : {{age}}</div>
</template>

<script>
  export default {
    name: "Sub",
    props: ["name", "age"],
    created: function () {},
  };
</script>

<style scoped></style>
```

```html
<!--App.vue-->
<template>
  <div id="app">
    <sub v-bind:name="kukaro" :age="27"></sub>
  </div>
</template>

<script>
  import Sub from "./components/Sub";

  export default {
    name: "app",
    components: {
      Sub,
    },
    data() {
      return {};
    },
  };
</script>

<style></style>
```

- App.vue에서 Sub.vue를 사용하려면 import / components / div 에 명시해야함
- **props 는 readonly !!**
- props 는 객체 표시 권장
- v-bind로 묶어서 전송 가능

### event : 하위 컴포넌트에서 상위 컴포넌트로 데이터를 전송할 때 event를 사용해야 함

```javascript
// 하위 컴포넌트 : childComponent
var childComponent = {
  methods: {
    sendEvent: function () {
      this.$emit("update");
    },
  },
};

// 상위 컴포넌트 : root 컴포넌트
new Vue({
  el: "#app",
  components: {
    "child-component": childComponent,
  },
  methods: {
    showAlert: function () {
      alert("event received");
    },
  },
});
```

```html
<div id="app">
  <child-component v-on:update="showAlert"></child-component>
</div>
```

- childComponent에서 sendEvent() 메서드가 실행되면 update 이벤트가 발생되고, 이를 상위 컴포넌트의 v-on 으로 받아 showAlert() 메서드를 실행
