<template>
<div class="login-form">
    <img class="logo" alt="Vue logo" src="../assets/restor-logo.png">
    <h2>Login</h2>
    <div class="login">
        <input type="email" v-model="email" placeholder="Email">
        <input type="password" v-model="password" placeholder="Password">
        <button v-on:click="Login">Login</button>
        <p>Don't have account,
            <router-link to="/sign-up">SignUp</router-link>
        </p>
    </div>
</div>
</template>

<script>
import axios from 'axios'
export default {
    name: "LoginPage",
    data() {
        return {
            email: '',
            password: ''
        };
    },
    methods: {
        async Login() {
            console.warn('yes', this.email, this.password);
            let result = await axios.get(
                `http://localhost:3000/users?email=${this.email}&password=${this.password}`
                );
                console.warn(result);
            if (result.status == 200 && result.data.length > 0) {
                localStorage.setItem("user-info", JSON.stringify(result.data[0]));

                this.$router.push({ name: 'Home' })

                console.warn('yes');
            }
        },
    },
    mounted() {
        let user = localStorage.getItem('user-info');
        if (user) {
            this.$router.push({ name: 'Home' })
        }
    },
}
</script>

<style>
.signUp {
    border: 1px solid skyblue;
    width: 320px;
    border-radius: 10px;
    box-shadow: 1px 1px 1px 1px rgba(102, 101, 101, 0.2);
    background-color: rgb(230, 225, 225);
    margin-left: auto;
    margin-right: auto;
    padding: 20px;
}

.logo {
    height: 120px;
}

.register input {
    width: 300px;
    height: 30px;
    padding: 3px;
    text-align: center;
    border-radius: 10px;
    display: block;
    margin-bottom: 10px;
    margin-left: auto;
    margin-right: auto;
    border: 1px solid skyblue;
}

.register button {
    width: 300px;
    height: 40px;
    color: white;
    border-radius: 10px;
    border: 1px solid skyblue;
    background-color: skyblue;
}
</style>
