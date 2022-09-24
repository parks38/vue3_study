# vue3-project

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).


### Reactive vs. Ref

둘다 반응형 상태 선언하기 
- 반응형이란? call by reference 으로 값이 변화 되었을때 값을 모두 변경 적용 

> ref 
독립적인 값 (문자열) 반응형으로 생성하기. 
ref 는 반응형이면서 변이가능한(mutable) 객체를 반환합니다. 현재 갖고 있는 내부의 값에 대한 반응형 참조(reference)의 역할을 하며, 
여기서 이름이 유래되었습니다. 이 객체는 오직 value 이라는 하나의 속성만 포함합니다.
```js
import { ref } from 'vue'

const count = ref(0)
console.log(count.value) // 0

count.value++
console.log(count.value) // 1
```

반응형 상태 선언하기
JavaScript 객체에서 반응형 상태를 생성하기 위해, reactive 메서드를 사용할 수 있습니다.
```js
import { reactive } from 'vue'

// 반응형 상태
const state = reactive({
  count: 0
})
```
이것이 바로 Vue 의 반응형 시스템의 본질입니다. 컴포넌트의 data() 에서 객체를 반환할 때, 
이것은 내부적으로 reactive() 에 의해 반응형으로 만들어집니다. 템플릿은 이러한 반응형 속성을 사용하는 렌더 함수 로 컴파일됩니다.


```js
const App = {
  setup() {
    const person = {name: 'John'};
    const personRef = ref({name: 'John'});
    const personReactive = reactive({name: 'John'});
    const changeName = (name) => {
      person.name = name;
      personRef.value.name = name;
      personReactive.name = name;
    }
    return {
      changeName,
      person,
      personRef,
      personReactive,
    }
  }
}

// example 2 
const count = ref(1)
const obj = reactive({ count })

// ref 가 풀림(unwrap)
console.log(obj.count === count.value) // true

// `obj.count`를 갱신함
count.value++
console.log(count.value) // 2
console.log(obj.count) // 2

// `count` ref를 갱신함
obj.count++
console.log(obj.count) // 3
console.log(count.value) // 3
```