<script setup>
import Navbar from '../components/Navbar.vue';
import { useRouter } from 'vue-router';
import { useAuthStore } from "@/stores/auth"
import { ref } from 'vue';

const authStore = useAuthStore()
const router = useRouter()

const username = ref("")
const password = ref("")

const isLogin = ref(null)

const login = async() => {
    const response = await fetch("http://localhost:3000/users/", {
        method: "post",
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({
            username: username.value,
            password: password.value
        })
    })
    const data = await response.json()
    console.log(data)
    if (data.message == "login success"){
        authStore.username = username.value
        authStore.password = password.value
    
        isLogin.value = true
    
        router.push("/")
    }
    else {
        isLogin.value = false
    }
}

</script>

<template>
    <Navbar />
    <div class="content p-8 flex flex-col gap-4">
        <div class="font-bold text-xl">Login Page</div>
        <form action="" class="flex flex-col gap-4 w-fit">
            <input type="text" class="p-2 text-base border outline-none" placeholder="Username" v-model="username">
            <input type="password" class="p-2 text-base border outline-none" placeholder="Password" v-model="password">
            <div v-if="isLogin === false" class="font-bold text-red-500 text-sm">username/password salah</div>
            <button type="button" class="bg-blue-400 p-2" @click="login">Login</button>
        </form>
    </div>
</template>