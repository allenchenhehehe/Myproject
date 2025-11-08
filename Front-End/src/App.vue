<script setup>
import { ref, onMounted, computed } from 'vue'
import Login from './components/Users/Login.vue'
import SignUp from './components/Users/SignUp.vue'
import Navbar from './components/Users/Navbar.vue'
import ForgetPassword from './components/Users/ForgetPassword.vue'
import Home from './components/Users/Task/Home.vue'
import MyFridge from './components/Users/Task/MyFridge.vue'
import Recipes from './components/Users/Task/Recipes.vue'
import ShoppingList from './components/Users/Task/ShoppingList.vue'
import { STATUS_LOGIN, STATUS_SIGNUP, STATUS_APP, STATUS_FORGET_PASSWORD, STATUS_FRIDGE } from './libs/constants'
const status = ref(STATUS_LOGIN)
const currentPage = ref('Home')
const gotoSignup = () => (status.value = STATUS_SIGNUP)
const gotoLogin = () => (status.value = STATUS_LOGIN)
const gotoApp = () => (status.value = STATUS_APP)
const handlePageChange = (pageName) => {
    currentPage.value = pageName
}
const currentPageComponent = computed(() => {
    switch (currentPage.value) {
        case 'Home':
            return Home
        case 'My Fridge':
            return MyFridge
        case 'Recipes':
            return Recipes
        case 'Shopping List':
            return ShoppingList
        default:
            return Home
    }
})
const gotoForget = () => (status.value = STATUS_FORGET_PASSWORD)
</script>

<template>
    <Login @signup="gotoSignup" @navbar="gotoApp" @forgetpassword="gotoForget" v-if="status == STATUS_LOGIN" />
    <SignUp @login="gotoLogin" v-if="status == STATUS_SIGNUP" />
    <ForgetPassword @login="gotoLogin" v-if="status == STATUS_FORGET_PASSWORD" />
    <div v-if="status == STATUS_APP" class="min-h-screen bg-[#fefae0] text-gray-800 overflow-x-hidden">
        <Navbar :currentPage="currentPage" @change-page="handlePageChange" />
        <component :is="currentPageComponent" />
    </div>
</template>
