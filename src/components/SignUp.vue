<template>
    <div class="signUp-form">
        <img class="logo" alt="Vue logo" src="../assets/restor-logo.png">
        <h2>Sign Up</h2>
        <div class="register">
            <input type="text" v-model="name" placeholder="Name">
            <input type="email" v-model="email" placeholder="Email">
            <input type="password" v-model="password" placeholder="Password">
            <button v-on:click="signUp">Sign Up</button>
            <p> Already have
                <router-link to="/login">Login</router-link>
            </p>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'SignUp',
    data() {
        return {
            name: '',
            email: '',
            password: '',
        }
    },
    methods: {
        async signUp() {
            console.warn("yes", this.name, this.email, this.password);
            let result = await axios.post("http://localhost:3000/users", {
                name: this.name,
                email: this.email,
                password: this.password,
            });
            console.warn(result);
            if (result.status == 201) {
                localStorage.setItem("user-info", JSON.stringify(result));
                this.$router.push({ name:'Home'})
            }
        }
    },
    mounted() {
        let user = localStorage.getItem('user-info');
        if (user) {
                this.$router.push({ name: 'Home' })
        }
    }
}
</script>

<style>

</style>
