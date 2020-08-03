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