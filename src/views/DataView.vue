<script setup>
import Navbar from '../components/Navbar.vue';
import { useAuthStore } from '../stores/auth';

const { username } = useAuthStore()

const data = [
    {
        name: "Book",
        quantity: 7
    },
    {
        name: "Pen",
        quantity: 2
    },
    {
        name: "Sciccors",
        quantity: 1
    }
]

</script>

<template>
    <Navbar />
    <div class="content flex flex-col gap-4 w-1/2 p-8">
        <div v-if="username === ''" class="text-xl">Anda harus login dulu untuk melihat halaman ini</div>
        <div v-else class="data">
            <div class="font-bold text-2xl">Data</div>
            <table class="border-collapse w-full">
                <tr>
                    <td>No.</td>
                    <td>Name</td>
                    <td>Quantity</td>
                </tr>
                <tr v-for="(item, index) in data">
                    <td>{{ index + 1 }}</td>
                    <td>{{ item.name }}</td>
                    <td>{{ item.quantity }}</td>    
                </tr>
            </table>
        </div>
    </div>
</template>

<style>
th, td{
    border: 1px solid #ccc;
    padding: 0.5rem;
}
</style>