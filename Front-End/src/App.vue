<script setup>
import { ref, onMounted } from 'vue'
import Login from './components/Users/Login.vue'
import SignUp from './components/Users/SignUp.vue'
import AppHeader from './components/AppHeader.vue'
import ForgetPassword from './components/Users/ForgetPassword.vue'
import { STATUS_LOGIN, STATUS_SIGNUP, STATUS_NAVBAR, STATUS_FORGET_PASSWORD } from './libs/constants'
const status = ref(STATUS_LOGIN)
const gotoSignup = () => (status.value = STATUS_SIGNUP)
const gotoLogin = () => (status.value = STATUS_LOGIN)
const gotoNavbar = () => (status.value = STATUS_NAVBAR)
const gotoForget = () => (status.value = STATUS_FORGET_PASSWORD)
</script>

<template>
    <div class="min-h-screen bg-[#fefae0] text-gray-800 overflow-x-hidden">
        <Login @signup="gotoSignup" @navbar="gotoNavbar" @forgetpassword="gotoForget" v-if="status == STATUS_LOGIN" />
        <SignUp @login="gotoLogin" v-if="status == STATUS_SIGNUP" />
        <AppHeader v-if="status == STATUS_NAVBAR" />
        <ForgetPassword @login="gotoLogin" v-if="status == STATUS_FORGET_PASSWORD" />
    </div>
</template>
