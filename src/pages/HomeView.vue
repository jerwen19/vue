<template>
    <div class="shadow-xl w-3/6 bg-gray-200 p-6 rounded-xl">
        <div class="text-left">
            <h1 class=" bg-green-600 text-gray-50 inline-block p-2 rounded-md"> List of Username</h1>
        </div>
        <p v-if="usersList.length === 0">No user found</p>
        <ul class="" v-for="user in usersList" :key="user._id">

            <li class="flex justify-between items-center">
                <router-link v-if="user && user._id" :to="{ name: 'user-profile', params: { id: user._id } }">
                    {{ user.username }}


                </router-link>
                <span v-if="user._id" @click="deleteUserHandler(user._id)"
                    class="bg-red-700 cursor-pointer inline-block p-2 rounded-full text-gray-50">X</span>
            </li>

        </ul>

        <router-link class="bg-blue-600 cursor-pointer rounded-lg p-3 inline-block text-gray-50"
            :to="{ name: 'registration' }">Register
            User</router-link>
    </div>


</template>

<script setup>
import { onMounted, ref } from 'vue'
import axiosClient from '../axiosClient'

const usersList = ref([])
const username = ref('')
const password = ref('')
const isError = ref(false)

onMounted(async () => {
    await getUsers()
})

const getUsers = async () => {
    isError.value = false;
    try {
        const response = await axiosClient.get('/getUsers')
        usersList.value = response.data.usersList;
    } catch (err) {
        console.log(err.message)
    }
}

const deleteUserHandler = async (id) => {
    try {
        const response = await axiosClient.delete('/deleteUser/' + id)
        console.log(response)
        usersList.value = usersList.value.filter(user => user._id !== id);
    } catch (err) {
        console.log(err.message)
    }
}


</script>

<style></style>