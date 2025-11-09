<script setup>
import { ref, onMounted, computed } from 'vue'
import Login from './components/Users/Login.vue'
import SignUp from './components/Users/SignUp.vue'
import Navbar from './components/Users/Navbar.vue'
import ForgetPassword from './components/Users/ForgetPassword.vue'
import Home from './components/ApplicationSection/Home.vue'
import MyFridge from './components/ApplicationSection/MyFridge.vue'
import Recipes from './components/ApplicationSection/Recipes.vue'
import ShoppingList from './components/ApplicationSection/ShoppingList.vue'
import { STATUS_LOGIN, STATUS_SIGNUP, STATUS_APP, STATUS_FORGET_PASSWORD } from './libs/constants'
const status = ref(STATUS_LOGIN)
const currentPage = ref('Home')
const gotoSignup = () => (status.value = STATUS_SIGNUP)
const gotoLogin = () => (status.value = STATUS_LOGIN)
const gotoApp = () => (status.value = STATUS_APP)
const handlePageChange = (pageName) => {
    currentPage.value = pageName
}
const gotoForget = () => (status.value = STATUS_FORGET_PASSWORD)
</script>

<template>
    <Login @signup="gotoSignup" @navbar="gotoApp" @forgetpassword="gotoForget" v-if="status == STATUS_LOGIN" />
    <SignUp @login="gotoLogin" v-if="status == STATUS_SIGNUP" />
    <ForgetPassword @login="gotoLogin" v-if="status == STATUS_FORGET_PASSWORD" />
    <div v-if="status == STATUS_APP" class="min-h-screen bg-[#fefae0] text-gray-800 overflow-x-hidden">
        <Navbar @change-page="handlePageChange" />
        <Home v-if="currentPage == 'Home'" />
        <MyFridge v-if="currentPage == 'My Fridge'" />
        <Recipes v-if="currentPage == 'Recipes'" />
        <ShoppingList v-if="currentPage == 'Shopping List'" />
    </div>
</template>
