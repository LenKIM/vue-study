![image-20200731102501462](https://tva1.sinaimg.cn/large/007S8ZIlgy1gh9w9ztmsxj30r50exac7.jpg)

View - HTML?

ViewModel - Vue

Model - Plain JavaScript Objects



![image-20200731104155989](https://tva1.sinaimg.cn/large/007S8ZIlgy1gh9wri3wbbj30rz0blgnl.jpg)





즉시 실행 함수 - (function() {})

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app"></div>

<script>
    var div = document.querySelector('#app');
    var viewModel = {};

    // Object.defineProperty(대상 객체, 객체의 속성, {
    //     //정의할 내용
    // })
    //즉시 실행 함수
    (function () {
        function init() {
            Object.defineProperty(viewModel, 'str', {
                get() {
                    console.log('접근')
                },
                set(v) {
                    console.log('할당', v)
                    render(v)
                }
            })
        }
        function render(v) {
            div.innerHTML = v;
        }

        init();
    })();
</script>
</body>
</html>
```



## 1. 인스턴스 생성

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>

<body>
    <div id="app">
        {{ message }}
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

    <script>
        var vm = new Vue({
          data: {
            message: 'hi'
          }
        });
    </script>
</body>
</html>
```



![image-20200731112802942](https://tva1.sinaimg.cn/large/007S8ZIlgy1gh9y3ht5cxj30g50j6acr.jpg)



## 2. 인스턴스와 생성자 함수

자바 스크립트에서 

```javascript
function Person(name, job){
	this.name = name;
	this.job = job;
}
// undefined
var p = new Person('josh', 'dev')
// undefined
```



왜 new Vue 안에 함수로 작성하는가?

**매번 함수를 정의하는 것이 아니라, 정의된 함수를 갖고와서 쓸 수 있다.**



![image-20200731115239209](https://tva1.sinaimg.cn/large/007S8ZIlgy1gh9yt2sh0kj30gv0cpjuo.jpg)



## 3. 뷰 컴포넌트

재사용성?

![image-20200731115535256](https://tva1.sinaimg.cn/large/007S8ZIlgy1gh9yw4t9xhj30iw0bc400.jpg)



컴포넌트 간에 관계가 설정된다.



## 4. 전역 컴포넌트

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <app-header>
    </app-header>
    <app-content></app-content>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

<script>
    // Vue.component('컴포넌트 이름', 컴포넌트 내용)
    Vue.component('app-header', {
        template: '<h1>Header</h1>'
    })

    Vue.component('app-content', {
        template: '<h1>aapp-content</h1>'
    })

    new Vue({
        el: '#app',
        data: {
            message: 'hi'
        },
    });
</script>
</body>
</html>
```

## 5. 지역 컴포넌트

서비스를 만들 때 가장 많이 쓰는 방법을 활용해보자.

```html
<body>
<div id="app">
    <app-header>
    </app-header>
    <app-content></app-content>
    <app-footer/>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

<script>
    // 전역 설정 Vue.component('컴포넌트 이름', 컴포넌트 내용)
    Vue.component('app-header', {
        template: '<h1>Header</h1>'
    })

    Vue.component('app-content', {
        template: '<h1>aapp-content</h1>'
    })

    new Vue({
        el: '#app',
        //지역 컴포넌트 등록 방식
        components: {
            // '컴포넌트 이름':'컴포넌트 내'
            'app-footer': {
                template: '<footer>footer</footer>'
            }

        },
        data: { aa : "a"}

    });
```



지역컴포넌트와 전역컴포넌트의 차이가 무엇일까?

왜 따로 쓰는걸까?

`new Vue({components: ??})`

*지역은 하단에 어떤 것이 정의됐는지 알 수 있다. 따라서 실무에서는 아래 계속 추가하는 방식으로 사용한다.*



## 6. 컴포넌트와 인스턴스의 관계

전역컴포넌트는 다른 인스턴스에서 사용 가능하나, 지역 컴포넌트는 사용 불가

## 컴포넌트 통신 방법

컴포넌트 큰거 하나가 나눠진다.

나눠지게 되면 규칙이 생긴다.

![image-20200731134011048](https://tva1.sinaimg.cn/large/007S8ZIlgy1gha1wyw6c3j30fm0bmabc.jpg)



상위 컴포넌트 > 하위 컴포넌트  =====> props 전달

하위 컴포넌트 > 상위 컴포넌트 =====> 이벤트 발생



![image-20200731134307482](https://tva1.sinaimg.cn/large/007S8ZIlgy1gha200yuovj30fv0bkq3d.jpg)

![image-20200731134520159](/Users/len/Library/Application Support/typora-user-images/image-20200731134520159.png)

내려가는 데이터는 `Props` 라는 이름으로 내려간다.

아래에서 위로 올라가는 것은 `Event` 라고 한다.

![image-20200731134614027](https://tva1.sinaimg.cn/large/007S8ZIlgy1gha239o5cyj30fn0a33yz.jpg)

## Props

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <div id="app">
        <app-header
<!--                v-bind:프롭스 속성이름="상위 컴포넌트의 데이터 이름"-->
                v-bind:prosdata="message"
        ></app-header>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

    <script>
        var appHeader = {
            template: '<h1>header</h1>',
            props: ['prosdata']
        }

        new Vue({
            el: '#app',

            components: {
                'app-header': appHeader
            },
            data: {
                message: 'h1'
            }
        });
    </script>
</body>
</html>
```



Props 의 특징을 한 번 짚고 넘어가자. 

***Reactivity 가 상위에서 하위로 props로 데이터가 넘어간다.***

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <div id="app">
        <app-header
                v-bind:propsdata="message"
        ></app-header>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

    <script>
        var appHeader = {
            template: '<h1>{{ propsdata }}</h1>',
            props: ['propsdata']
        }

        new Vue({
            el: '#app',

            components: {
                'app-header': appHeader
            },
            data: {
                message: 'h1'
            }
        });
    </script>
</body>
</html>
```



## 8. Event-emit

이벤트는 하위 컴포넌트에서 emit을 발생시켜 상위 컴포넌트에서 이를 캐치한다.

하위 컴포넌트에서 메서드를 정의하고 template에 해당 메소드의 명을 입력한다.

이후에, 

```java
<!--<app-header v-on:하위 컴포넌트에서 발생한 이벤트 이="상위 컴포넌트 이벤트 이름"></app-header>-->
```

상위 컴포넌트에서는 위와 같은 형태의 입력을 따른다.

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <!--        <app-header v-on:하위 컴포넌트에서 발생한 이벤트 이="상위 컴포넌트 이벤트 이름"></app-header>-->
    <p>{{ num }}</p>
    <app-header v-on:pass="logText"></app-header>
    <app-content v-on:increase="increaseNumber"></app-content>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

<script>
    var appHeader = {
        template: '<button v-on:click="passEvent">click me</button>',
        methods: {
            passEvent: function () {
                this.$emit('pass')
            }
//하위 컴포넌트에서 pass라는 이벤트가 emit 되면 상위 컴포넌트가 pass를 잡고 logText를 실행한다.
        }
    }
    var appContent = {
        template: '<button v-on:click="addNumber">add</button>',
        methods: {
            addNumber: function () {
                this.$emit('increase')
            }
        }
    }
    new Vue({
        el: '#app',
        components: {
            'app-header': appHeader,
            'app-content': appContent
        },
        methods: {
            logText: function () {
                console.log('Hi')
            },
            increaseNumber: function () {
                this.num = this.num + 1;
            }
        },
        data: {
            num: 10
        }
    });
</script>
</body>
</html>
```

---

## vue에서의 this

https://www.w3schools.com/js/js_this.asp

https://medium.com/better-programming/understanding-the-this-keyword-in-javascript-cb76d4c7c5e8



## 같은 레벨의 인스턴스사이에 어떻게 통신하는가?

![image-20200801113833632](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghb40rn1qxj30iu0cowfa.jpg)

`AppContent` 에서 `AppHeader` 로 데이터(10)를 전달하는 법을 이해해보자.

같은 레벨상에서 10으로 바로 전달 할수 없어서 Root 로 10을 보내고나서 Root에서 AppHeader로 보내자

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <app-header></app-header>
    <app-content v-on:pass="deliverNum(value)"></app-content>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>

    var appHeader = {
        template: '<div>header</div>'
    }

    var appContent = {
        template: '<div>appContent<button v-on:click="passNum">pass</button></div>',
        methods: {
            passNum: function () {
                this.$emit('pass', 10);
            }
        }

    }

    new Vue({
        el: '#app',
        components: {
            'app-header': appHeader,
            'app-content': appContent
        },
        data: {
            num: 0
        },
        methods: {
            //value가 emit을 통해 넘어온 10이 암묵적으로 넘어온다.
            deliverNum: function (value) {
                this.num = value;
            }
        }
    })

</script>
</body>
</html>
```

Root까지 암흑적으로 10이라는 데이터를 넘겼다.

![image-20200801121106760](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghb4yliddej30ho0c6gmo.jpg)

루트를 통해서 `AppHeader` 또는 상위 컴포넌트를 통해서 데이터를 넘겨준다.

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <!--    <app-header v-bind:프롭스 속성 이름="상위 컴포넌트의 속성"></app-header>-->
    <app-header v-bind:propsdata="num"></app-header>
    <!--    <app-header></app-header>-->
    <app-content v-on:pass="deliverNum"></app-content>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>

    var appHeader = {
        template: '<div>header</div>',
        props: ['propsdata']

    }

    var appContent = {
        template: '<div>appContent<button v-on:click="passNum">pass</button></div>',
        methods: {
            passNum: function () {
                this.$emit('pass', 10);
            }
        }

    }

    new Vue({
        el: '#app',
        components: {
            'app-header': appHeader,
            'app-content': appContent
        },
        data: {
            num: 0
        },
        methods: {
            //value가 emit을 통해 넘어온 10이 암묵적으로 넘어온다.
            deliverNum: function (value2) {
                this.num = value2;
            }
        }
    })
</script>
</body>
</html>
```

## Vue-router

뷰라이터는 뷰라이러리르 이용하여 싱글페이지 애플 구현할 때 사용하는 라이브러리

https://router.vuejs.org/kr/

기본 형태는 아래와 같다.

```vue
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
<!--div#app + tab-->
    <div id="app">

    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script src="https://unpkg.com/vue-router@2.0.0/dist/vue-router.js"></script>

    <script>
        var Router = new VueRouter({

        });
        new Vue({
            el: '#app',
            router: Router
        })
    </script>
</body>
</html>
```



### 라우터가 표시되는 영역 및 router-view 태그 설명

```vue
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
<!--div#app + tab-->
<div id="app">
    <router-view></router-view>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script src="https://unpkg.com/vue-router@2.0.0/dist/vue-router.js"></script>

<script>
    var LoginComponent = {
        template: '<div>login</div>'
    };
    var MainComponent = {
        template: '<div>main</div>'
    };
    var Router = new VueRouter({
        //페이지의 라우딩 정보
        routes: [ // 각 페이지의 정보를 객체로 넣습니다.
            {
                //페이지의 Url
                path: '/login',
                // 해당 url에서 표시될 컴포넌트
                component: LoginComponent
            },
            {
                path: '/main',
                component: MainComponent
            }
        ]

    });
    new Vue({
        el: '#app',
        router: Router
    })
</script>
</body>
</html>
```

### 링크를 이용한 페이지 이동 및 router-link 태그

사용자가 링크를 통해 이동하게 하는 태그

```vue
<!--div#app + tab-->
<div id="app">
    <!--    router-link*2 + tab -->
    <div>
        <router-link to="/login">Login</router-link>
        <router-link to="/main">Main</router-link>
    </div>
    <router-view></router-view>
</div>

```

와 같이 하면 이동할 수 있는 `<a href=/login>` 을 만들어 준다.



[네비게이션 가드 블로그 글 안내](https://joshua1988.github.io/web-development/vuejs/vue-router-navigation-guards/)



## HTTP 통신 라이브러리 axios

Ajax 는 비동기적인 웹 애플리케이션의 제작을 위한 개발 기법

[Ajax 위키백과 링크](https://ko.wikipedia.org/wiki/Ajax)

[Vue Resource 깃헙 주소](https://github.com/pagekit/vue-resource)

vue에서 원래 vue resource가 있었음. 그리고 그 라이브러리가 vue.js에서 활용할 수 있는 공식 라이브러리였다.



Vue에서 권하는 HTTP 통신 라이브러는 액시오스



[Axios 깃헙 주소](https://github.com/axios/axios)

[자바스크립트 비동기 처리와 콜백 함수](https://joshua1988.github.io/web-development/javascript/javascript-asynchronous-operation/)

[자바스크립트 Promise 이해하기](https://joshua1988.github.io/web-development/javascript/promise-for-beginners/)

[자바스크립트 async와 await](https://joshua1988.github.io/web-development/javascript/js-async-await/)



실제 활용해보자.

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

<body>
<div id="app">
    <button v-on:click="getData">get user</button>
    <div>
        적용되어진 {{ users }}
    </div>
</div>
<div>
    적용되어 지지 않은 {{ users }}
</div>
<script>
    new Vue({
        el: '#app',
        data: {
            users: []
        },
        methods: {
            getData: function () {
                // 1. this
                var vm = this;
                axios.get('https://jsonplaceholder.typicode.com/todos')
                    .then(function (response) {
                        console.log(response.data)
                        vm.users = response.data;
                        // 2. 이 안에 this는 비동기 처리에 해당하는 부분에 해당한다.
                    }).catch(function (error) {
                    console.log(error)
                })
            }
        }
    })
</script>
</body>
</html>
```



## 웹 서비스에서의 클라이언트와 서버와의 HTTP 통신 구조

![image-20200802155333715](https://tva1.sinaimg.cn/large/007S8ZIlgy1ghch0el6jij311q0hs76r.jpg)

[프런트엔드 개발자가 알아야 하는 HTTP 프로토콜](https://joshua1988.github.io/web-development/http-part1/)

[구글 크롬 개발자 도구 공식 문서](https://developers.google.com/web/tools/chrome-devtools/)

---

## 템플릿 문법 - 기본

`v-bind`

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <div id="app">
        <p v-bind:id="uuid">{{ num }}</p>
        <p v-bind:class="name">{{ doubleNum }}</p>
        <div v-if="loading">Loading...</div> DOM을 완전 제거
        <div v-else>test user has been logged in</div>
        <div v-show="loading">Loading.....</div> DOM을 CSS로 변경
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

    <script>
        new Vue({
            el: '#app',
            data: {
                str: 'hi',
                num: 10,
                uuid: 'abc1234',
                name: "className",
                loading: true
            },
            computed: { // data의 데이터를 재활용할 때 사용할 수 있다.
                doubleNum: function () {
                    return this.num * 2;
                }
            }
        })
    </script>
</body>
</html>
```



모르는 문법이 나왔을 때 공식 문서를 보고 해결하는 방법



Vue 공식 홈페이지에서 검색하기.

https://vuejs.org/v2/guide/forms.html#Text

## Watch	

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    {{ num }}
    <button v-on:click="addNum">increase</button>
</div>
    <script src="https://unpkg.com/vue"></script>
    <script>
        new Vue({
            el: '#app',
            data: {
                num: 10
            },
            watch: {
                //num 의 상태가 바뀔때마다 실행된다.
                num: function () {
                    this.logText()
                }
            },
            methods:{
                addNum: function () {
                    this.num = this.num + 1
                },
                logText: function () {
                    console.log("log changed")
                }
            }
        })
    </script>
</body>
</html>
```



## watch와 compute의 차이는?

공식 사이트 - https://vuejs.org/v2/guide/computed.html#ad

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    {{ num }}
    <button v-on:click="addNum">increase</button>
</div>
<script src="https://unpkg.com/vue"></script>
<script>
    new Vue({
        el: '#app',
        data: {
            num: 10
        },
        computed: {
            //데이터의 의존성이 달려있다. 벨리데이션, 간단 연산 로직
            doubleNum: function () {
                return this.num * 2
            }
        },
        watch: {
            // 무거운 로직을 실행할 경우 watch를 실행한다.
            //num 의 상태가 바뀔때마다 실행된다.
            num: function (newValue, oldValue) {
                this.fetchUserByNumber(newValue);
            }
        },
        methods: {
            fetchUserByNumber: function(num){
                console.log(num)
            },
            addNum: function () {
                this.num = this.num + 1
            },
            logText: function () {
                console.log("log changed")
            }
        }
    })
</script>
</body>
</html>
```

[Where does npm install packages? 스택 오버 플로우 글](https://stackoverflow.com/questions/5926672/where-does-npm-install-packages)



# Vue-CLI

[Vue CLI 2.x]

Vue init '프로젝트 템플릿 유형' '프로젝트 폴더 위치'

[Vue CLI 3.x]

vue create '프로젝트 폴더 위치'



## Vue-CLI 로 나온 프로젝트 이해하기.

`npm run serve`



```vue
new Vue({
  el:"#app"
})

new Vue({
}).$mount('#app')
```

`  render: h => h(App),` 의 의미는 템플릿이라고 생각하면 된다.

render > Vue 내부에서 사용하는 함수



## 싱글파일 컴포넌트

- template 에는 무조건 하나의 div 루트가 존재해야한다.
- 컴포넌트 이름은 최소 2개 단어의 합성으로 만들어진다.
- 컴포넌트 등록 방법은?

```vue
App.vue
<!--템플릿패턴은 div가 기본적으로 하나만 존재해야 한다.-->
<template>
    <div>
<!--        <app-header v-bind:프롭스 속성 이름="상위 컴포넌트의 데이터 이름"></app-header>-->
        <app-header v-bind:propsdata="str"></app-header>
        {{ str }}
    </div>
</template>

<script>
import AppHeader from "@/components/AppHeader";

    export default {
        data: function () {
            return {
                str: "hi"
            }
        },
        components: {
            'app-header': AppHeader
        }

    }
</script>
<style>
</style>
```

```vue
<template>
    <header>
        <h1>Header</h1>
    </header>
</template>
<script>
    export default {
        name: "AppHeader",
        props: ['propsdata']
    }
</script>
<style scoped>
</style>
```

- event emit 구현

```vue
<template>
    <header>
        <h1>{{ propsdata }}</h1>
        <button v-on:click="sendEvent"> send </button>
    </header>
</template>

<script>
    export default {
        name: "AppHeader",
        props: ['propsdata'],
        methods: {
            sendEvent: function () {
                // 상위에서 정의한 이벤트를 올렸을 경우
                this.$emit('renew')
            }
        }
    }
</script>
<style scoped>
</style>
```

```vue
<!--템플릿패턴은 div가 기본적으로 하나만 존재해야 한다.-->
<template>
    <div>
        <!--        <app-header v-bind:프롭스 속성 이름="상위 컴포넌트의 데이터 이름"></app-header>-->
        <app-header v-bind:propsdata="str"
                    v-on:renew="renewStr"></app-header>
        {{ str }}
    </div>
</template>

<script>
    import AppHeader from "@/components/AppHeader";

    export default {
        data: function () {
            return {
                str: "hi"
            }
        },
        components: {
            'app-header': AppHeader
        },
        methods: {
            renewStr: function () {
                this.str = 'Hello Vue'
            }
        }
    }
</script>
<style>
</style>
```

---

## 간단한 사용자 입력 폼 만들기

[이벤트 버블링과 캡쳐링 블로그 글](https://joshua1988.github.io/web-development/javascript/event-propagation-delegation/)

```vue
<template>
    <form v-on:submit="submitForm">
        <div>
            <label for="username">id: </label>
            <input id="username" type="text" v-model="username">
        </div>
        <div>
            <label for="password">pw: </label>
            <input id="password" type="password" v-model="password">
        </div>
        <button type="submit">login</button>
    </form>
</template>

<script>
    import axios from 'axios';

    export default {
        data: function () {
            return {
                username: '',
                password: '',
            }
        },
        name: "App",
        methods: {
            submitForm: function () {
                // 새로 고침을 막을 수 있음. 버블링을 막음.
                // event.preventDefault();
                // console.log(this.username, this.password)
                var url = 'https://jsonplaceholder.typicode.com/users'
                var data = {
                    username: this.username,
                    password: this.password
                }
                axios.post(url, data)
                    .then(function (response) {
                        console.log(response)
                    })
                    .catch(function (error) {
                        console.log(error)
                    })
            }
        }
    }
</script>
<style scoped>
</style>
```

With Axios

```vue
...
        methods: {
            submitForm: function () {
                // 새로 고침을 막을 수 있음. 버블링을 막음.
                // event.preventDefault();
                // console.log(this.username, this.password)
                var url = 'https://jsonplaceholder.typicode.com/users'
                var data = {
                    username: this.username,
                    password: this.password
                }
                axios.post(url, data)
                    .then(function (response) {
                        console.log(response)
                    })
                    .catch(function (error) {
                        console.log(error)
                    })
            }
        }
    }
</script>
```