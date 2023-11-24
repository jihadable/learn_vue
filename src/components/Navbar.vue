<script setup>
import { RouterLink, useRouter } from 'vue-router'
import { useAuthStore } from '../stores/auth';
import { ref } from 'vue';

const authStore = useAuthStore()
const isLogoutBtnShow = ref(false)
const router = useRouter()

const logout = () => {
    authStore.username = ""
    router.push("/login")
}

</script>

<template>
    <nav class="w-full flex items-center justify-between py-4 px-20 shadow-md bg-white">
        <div class="links flex gap-8 items-center">
            <RouterLink to="/">Home</RouterLink>
            <RouterLink to="/about">About</RouterLink>
            <RouterLink to="/data">Data</RouterLink>
        </div>
        <div v-if="authStore.username === ''" class="login-btn flex">
            <RouterLink to="/login" class="px-2 py-1 rounded bg-blue-400">Login</RouterLink>
        </div>
        <div v-else class="user relative">
            <div class="username px-2 py-1 rounded bg-blue-400 cursor-pointer" @click="isLogoutBtnShow=!isLogoutBtnShow">{{ authStore.username }}</div>
            <button v-if="isLogoutBtnShow" class="logout-btn absolute top-[105%] right-0 bg-white px-2 py-1 rounded border" @click="logout">Logout</button>
        </div>
    </nav>
</template>