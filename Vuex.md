## Vuex - 상태 관리 라이브러리

LoadMap

- 복잡한 애플리케이션의 컴포넌트들은 효율적으로 관리하는 Vuex라이브러리 소개
- Vuex 라이브러리의 등장배경인 Flux 패턴 소개
- Vuex 라이브러리의 주요 속성인 state, getters, mutations, actions 학습
- Vuex를 더 쉽게 코딩할 수 있는 방법인 Helper 기능 소개
- Vuex로 프로젝트를 구조화하는 방법과 모듈 구조화 방법 소개



목차

- Vuex 라이브러리 소개
- Flux 패턴 소개
- Vuex 컨셉과 구조
- Vuex 설치와 시작하기
- Vuex 기술 요소(statem getters, mutations, actions)
- Vuex Helpers
- Vuex로 프로젝트 구조화 및 모듈화하는 방법



![image-20200807133438721](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghi53e8mstj30mq0863zq.jpg)

![image-20200807134537257](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghi5erznqoj30qf0dz41g.jpg)

![image-20200807134903343](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghi5icssbnj30kd0dkac3.jpg)



`Controller` 가 `Model, View` 를 처리한다.

`Action` > `Dispatcher` > `Model` > `View`



![image-20200807135014109](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghi5jksy0sj30m50cxq5u.jpg)

![image-20200807135127784](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghi5kum9afj30n10b5406.jpg)

## Vuex 가 왜 필요한가?

[자바스크립트 비동기 처리와 콜백 함수 글 링크(클릭)](https://joshua1988.github.io/web-development/javascript/javascript-asynchronous-operation/) [자바스크립트 Promise 쉽게 이해하기 글 링크(클릭)](https://joshua1988.github.io/web-development/javascript/promise-for-beginners/)



![image-20200807135331397](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghi5mzt4woj30pg0bit9s.jpg)

![image-20200807135442684](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghi5o8dsmbj30qs0cu41l.jpg)

![image-20200807135607388](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghi5pp87suj30ql08h0tz.jpg)

## Vuex 컨셉

*단방향*

![image-20200807135656956](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghi5qkniecj30q00e7tbb.jpg)

![image-20200807135940858](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghi5teqw5fj30lh0dwgnr.jpg)

Actions - 비동기

Mutations - 동기 

State - 상태





## Vuex 기술 요소

![image-20200810083057679](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghld6cpc46j30j409a0uk.jpg)

비동기 처리 로직에 actions를 많이 사용한다.



### State란?

- 여러 컴포넌트 간에 공유할 데이터 - 상태

![image-20200810083259803](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghld8eu3ftj30r70e5tbc.jpg)

$store > 글로벌 펑션으로 정의되었기 때문에 사용 가능하다.

### getters란?

![image-20200810083401924](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghld9hrm1uj30q20c50vt.jpg)



### mutations란?

![image-20200810085856750](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghldzflwdaj30q50c2n0f.jpg)

첫번째 인자는 무조건 `state`이여야 한다.

`commit`이라는 것이 중요한데, `mutations`를 동작시키는 중요한 요소이다.



// 20

// 30



![image-20200810093317459](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghlez5rh71j30qe0cy780.jpg)



Vue.js 에 집중되던 부분을 todoInput 과 store 관계로 변화됨.



Vuex를 썼던 코드와 Vuex를 쓰지 않는 코드의 차이점을 이해하자.

중간에 App.vue의 의존도를 낮추자.





왜 Mutation을 커밋해야 되는지??

![image-20200810110131495](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghlhiz06u6j30r40e0n1a.jpg)



View 컴포넌트에서 commit을 했더니 바로 Mutations로 왔고, 그것이 state를 변경하는 행위로 이어졌다.



## Actions

![image-20200810110504928](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghlhmnzryhj30q00ecae8.jpg)

context의 의미는?

actions에서 mutations를 접근할 수 있습니다. 접근하기 위한 경로로 context가 제공되는 것이고, commit을 하면, 앞에서 우리가 했던 commit과 같은 행위를 하게 됩니다.

사용하는 쪽에서는 `dispatch` >  `delayDoubleNumber` > `doubleNumber` > `num`



![image-20200810110908865](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghlhqw9vlkj30r40dxadb.jpg)

![image-20200810111146677](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghlhtmh7oqj30q60e9djy.jpg)



### 왜 비동기 처리 로직은 actions에 선언해야 할까?

![image-20200810111653986](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghlhyyjufdj30pu0edtc6.jpg)

---

# Helper



어플리케이션이 커질때  모듈화를 어떻게 할 것인지???

![image-20200810112403517](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghli6esgqrj30oy0btjte.jpg)

![image-20200810112536450](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghli81h5drj30qk0cw0x5.jpg)

컴포넌트 로직단에서 사용할 수 있는가?

```
...mapState(['num'])  = this.$store.state.num

...mapGetters(['countedNum']) = this.$store.getters.countedNum

...

...mapMutations(['clickBtn']) = this.$store.mutations.clickBtn
```



## mapstate, mapGetters 소개, 왜 spread 연산자를 사용하는지?

![image-20200810113417866](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghlih25rwzj30qg0dyn06.jpg)

![image-20200810113628423](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghlijbtt0hj30qp0d2zo3.jpg)

왜 spread 연산자를 쓰는걸까?

원래 computed 속성이 있다. 고유의 컴퓨티드 속성을 써야 할 때가 많다.

기존의 computed와 mapGetters 를 한꺼번에 쓰기 위해서 사용된다.



### 리펙토링

1. getters로 접근하게 코드 수정 (다시 살펴보기) - this.storedTodoItems



![image-20200810114828681](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghlivtageyj30qa0eewi6.jpg)

![image-20200810115026653](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghlixv74q6j30n20dd77v.jpg)



헬퍼의 유연한 문법

![image-20200810115118641](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghliyrg7b0j30q10axtbo.jpg)



**리펙토링은 어떻게 했는가?**

mapGetters, mapMutations 를 리팩토링 한다.

```vue
import { mapGetters, mapMutations } from 'vuex'

export default {
  methods: {
    ...mapMutations({
      removeTodo: 'removeOneItem',
      //Payload 는 ??? 암묵적으로 html에서  넘겼다.
      toggleComplete: 'toggleOneItem'

    }),
    // removeTodo(todoItem, index) {
    //   this.$store.commit('removeOneItem', {todoItem, index});
    // },
    // toggleComplete(todoItem, index) {
    //   this.$store.commit('toggleOneItem', {todoItem, index});
    // }
  },
  computed: {
    // todoItems(){
    //   // 모두다 처리하고 깔끔하게 보이게 하는 것이 Vue의 의도이다.
    //   return this.$store.getters.storedTodoItems
    // }
    ...mapGetters(['storedTodoItems'])
  }
}
</script>

```



```vue
import { mapMutations } from 'vuex'

methods: {
  ...mapMutations({
    clearTodo: 'clearAllItems'
  }),
  // clearTodo: function (){
  //   this.$store.commit('clearAllItems')
  // }
}
```

`mapMutations` 으로 바로 넘김.



### 헬퍼 함수가 주는 간편함?



```vue
//Demo.vue
<template>
  <div id="root">
    <p>{{ originalPrice }}</p> 100
    <p>{{ doublePrice }}</p> 200
    <p>{{ triplePrice }}</p> 300
    권고되는 사항은 심플하게 코드되는 것
  </div>
</template>

<script>
import  { mapGetters } from 'vuex'
export default {
  name: "Demo",
  computed: {
    ...mapGetters(['originalPrice', 'doublePrice', 'triplePrice']),
    // 한번에 매핑시켜주는 효과를 가져다 준다.

    // originalPrice() {
    //   return this.$store.getters.originalPrice
    // },
    // doublePrice() {
    //   return this.$store.getters.doublePrice
    // },
    // triplePrice() {
    //   return this.$store.getters.triplePrice
    // }
  // computed 를 쓰지 않고 바로 접근할 경우 HTML 에서 길게 작성해야 할것이다.
  //
  }
}
</script>

<style scoped>

</style>
```

```vue
//DemoStore.js

import Vue from 'vue';
import Vuex from 'vuex';

Vue.use(Vuex);

export const store = new Vuex.Store({
    state: {
        price: 100
    },
    getters: {
        originalPrice(state){
            return state.price
        },
        doublePrice(state){
            return state.price * 2;
        },
        triplePrice(state){
            return state.price * 3;
        }
    }
})
```

