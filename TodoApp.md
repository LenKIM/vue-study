# # 컴포넌트 개발

src > components > component



**반응형 태그**



```html
<meta name="viewport" content="width=device-width,initial-scale=1.0">
```

반응형 웹에서 어떠한 디바이스이든 최적화된 화면을 보여주기 위한 기법이다.



**파비콘 설정**

구글폰트 설정

어썸폰트 설정



```vue
<style scoped>

</style>
```

의 의미는 해당 CSS는 여기서만 존재한다 라는 의미.



`TodoHeader` 개발 후 `TodoInput` 구현함.



![image-20200806135656566](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghh04ayegyj30gj0bq76n.jpg)



`localstorage` 로 구현시 문제점.

그러므로 아래와 같이 해결한다.

![image-20200806135752079](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghh057tm9cj30en0dtjt6.jpg)



---

사용자 개선 - 모달 컴포넌트

x-template 를 통해 모달을 만든다.

Slot? 

슬롯을 통해서 특정 부분을 재정의할 수 있다. 특정 컴포넌트의 일부 UI을 재사용할 수 있는 기능이다.



Slot 이라 작성된 부분은 추후 재정의할 수 있다.

```vue
<template>
  <transition name="modal">
    <div class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">

<!--          모달 헤더-->
          <div class="modal-header">
            <slot name="header">
              default header
            </slot>
          </div>
<!--          모달 바디-->
          <div class="modal-body">
            <slot name="body">
              default body
            </slot>
          </div>
<!--           모달 푸터-->
         <div class="modal-footer">
            <slot name="footer">
              default footer
              <button class="modal-default-button" @click="$emit('close')">
                OK
              </button>
            </slot>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>
...
```

위에 slot 되있는 부분을

```vue
//Todoinput.vue
<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <span class="addContainer">
      <i class="fas fa-plus " v-on:click="addTodo"></i>
    </span>

    <Modal v-if="showModal" @close="showModal = false">
      <!--
        you can use custom content here to overwrite
        default content
      -->
      <h3 slot="header">
        warnning!!
      </h3>
    </Modal>
  </div>
</template>
...
```

아래와 같이 재정의할 수 있다.

https://kr.vuejs.org/v2/examples/modal.html



## Trasnsitions&Animation

딱 두가지

구현관점과 사용관점

간단 이펙트를 바로바로 추가할 수 있다.

https://kr.vuejs.org/v2/guide/transitions.html