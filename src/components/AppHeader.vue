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