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