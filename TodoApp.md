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

