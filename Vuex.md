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

