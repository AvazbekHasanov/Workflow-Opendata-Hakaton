<script setup>
import {RouterLink} from "vue-router";
import {useRoute} from "vue-router";
import {ref, onMounted, reactive} from "vue";
import { getCurrentInstance } from 'vue';
import {data} from "autoprefixer";
import apiFetch from "@/utils/apiFetch.js";
import * as url from "node:url";
import router from "@/router/index.js";

const route = useRoute();

const errorMessages = reactive({
  email_error: 'Email address already exists!',
  is_show_email_error: false,
  role_error: 'Username address already exists!',
  is_show_role_error: false,
})

const userData = ref({
  user_id: route.params.user_id,
  login: '',
  password: '',
  email: '',
  remember_me: false
})

const { proxy } = getCurrentInstance();

const registerUser = async ()=>{
  for (let key in userData.value){
    if (!userData.value[key] && key != 'user_id') {
      console.log(userData.value)
      return
    }
  }
try{
    const url = '/auth/signup'
   const data = await apiFetch(url, {
     method: 'POST',
     headers: {
       'Content-Type': 'application/json',
     },
     body: JSON.stringify({"email": userData.value.email,
       "login": userData.value.login,
       "password": userData.value.password})
   })
  console.log("data dfsd", data)
  await router.push(`/auth/login`);

} catch(error) {
    console.error('There was an error!', error.response.data.typeError);

  };
}




</script>

<template>
<div class="font-[sans-serif] bg-white w-full h-full  flex items-center justify-center mx-auto md:h-screen p-4 dark:bg-gray-800">
      <div class="grid md:grid-cols-3 items-center shadow-[0_2px_10px_-3px_rgba(6,81,237,0.3)] rounded-xl overflow-hidden max-w-4xl">
        <div class="max-md:order-1 flex flex-col justify-center space-y-16 max-md:mt-16 min-h-full bg-gradient-to-r from-gray-900 to-gray-700 lg:px-8 px-4 py-4">
          <div>
            <h4 class="text-white text-lg font-semibold dark:text-gray-100">Create Your Account</h4>
            <p class="text-[13px] text-gray-300 mt-3 leading-relaxed dark:text-gray-100">Welcome to the employee registration page! Create your account to get started.</p>
          </div>
        </div>

        <form class="md:col-span-2 w-full py-6 px-6 sm:px-16" id="registration-form" @submit.prevent="handleSubmit">
          <div class="mb-6">
            <h3 class="text-gray-800 text-2xl font-bold dark:text-gray-100">Create Your Account</h3>
          </div>

          <div class="space-y-6">
            <div class="flex gap-2">

            <div class="w-1/2">
              <label class="text-gray-800 text-sm mb-2 block dark:text-gray-100">Login</label>
              <div class="relative flex items-center">
                <input name="name" type="text" v-model="userData.login" required class="text-gray-800 bg-white border border-gray-300 w-full text-sm px-4 pr-8 py-2.5 rounded-md
                 outline-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:text-white" placeholder="login" />
                <svg xmlns="http://www.w3.org/2000/svg" fill="#bbb" stroke="#bbb" class="w-4 h-4 absolute right-4" viewBox="0 0 24 24">
                  <circle cx="10" cy="7" r="6" data-original="#000000"></circle>
                  <path d="M14 15H6a5 5 0 0 0-5 5 3 3 0 0 0 3 3h12a3 3 0 0 0 3-3 5 5 0 0 0-5-5zm8-4h-2.59l.3-.29a1 1 0 0 0-1.42-1.42l-2 2a1 1 0 0 0 0 1.42l2 2a1 1 0 0 0 1.42 0 1 1 0 0 0 0-1.42l-.3-.29H22a1 1 0 0 0 0-2z" data-original="#000000"></path>
                </svg>
              </div>
            </div>

            <div class="w-1/2">
              <label class="text-gray-800 text-sm mb-2 block dark:text-gray-100">Password</label>
              <div class="relative flex items-center">
                <input name="name" type="text" v-model="userData.password" required class="text-gray-800 bg-white border border-gray-300 w-full text-sm px-4 pr-8 py-2.5 rounded-md outline-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:text-white" placeholder="password" />
                <svg xmlns="http://www.w3.org/2000/svg" fill="#bbb" stroke="#bbb" class="w-4 h-4 absolute right-4" viewBox="0 0 24 24">
                  <circle cx="10" cy="7" r="6" data-original="#000000"></circle>
                  <path d="M14 15H6a5 5 0 0 0-5 5 3 3 0 0 0 3 3h12a3 3 0 0 0 3-3 5 5 0 0 0-5-5zm8-4h-2.59l.3-.29a1 1 0 0 0-1.42-1.42l-2 2a1 1 0 0 0 0 1.42l2 2a1 1 0 0 0 1.42 0 1 1 0 0 0 0-1.42l-.3-.29H22a1 1 0 0 0 0-2z" data-original="#000000"></path>
                </svg>
              </div>
            </div>
            </div>


            <div>
              <label class="text-gray-800 text-sm mb-2 block dark:text-gray-100">Email address</label>
              <div class="relative flex items-center">
                <input name="email" type="email" v-model="userData.email" @input="errorMessages.is_show_email_error = false" required class="text-gray-800 bg-white border border-gray-300 w-full text-sm px-4 pr-8 py-2.5 rounded-md outline-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:text-white" placeholder="Enter email" />
                <svg xmlns="http://www.w3.org/2000/svg" fill="#bbb" stroke="#bbb" class="w-4 h-4 absolute right-4" viewBox="0 0 682.667 682.667">
                  <defs>
                    <clipPath id="a" clipPathUnits="userSpaceOnUse">
                      <path d="M0 512h512V0H0Z" data-original="#000000"></path>
                    </clipPath>
                  </defs>
                  <g clip-path="url(#a)" transform="matrix(1.33 0 0 -1.33 0 682.667)">
                    <path fill="none" stroke-miterlimit="10" stroke-width="40" d="M452 444H60c-22.091 0-40-17.909-40-40v-39.446l212.127-157.782c14.17-10.54 33.576-10.54 47.746 0L492 364.554V404c0 22.091-17.909 40-40 40Z" data-original="#000000"></path>
                    <path d="M472 274.9V107.999c0-11.027-8.972-20-20-20H60c-11.028 0-20 8.973-20 20V274.9L0 304.652V107.999c0-33.084 26.916-60 60-60h392c33.084 0 60 26.916 60 60v196.653Z" data-original="#000000"></path>
                  </g>
                </svg>
              </div>
              <span class="text-red-600" v-if="errorMessages.is_show_email_error">{{errorMessages.email_error}}  </span>
            </div>


            <div class="flex items-center select-none">
              <input id="remember-me" v-model="userData.remember_me" name="remember-me" type="checkbox" required class="h-4 w-4 shrink-0 text-blue-600 focus:ring-blue-500 pr-8 border-gray-300 rounded dark:bg-gray-700 dark:border-gray-600 dark:text-white" />
              <label for="remember-me" class="ml-3 block text-sm text-gray-800 dark:text-gray-100">
                I accept the <a href="javascript:void(0);" class="text-blue-600 font-semibold hover:underline ml-1 ">Terms and Conditions</a>
              </label>
            </div>
          </div>

          <div class="!mt-12">
            <button type="submit" @click="registerUser" class="w-full py-3 px-4 tracking-wider text-sm rounded-md text-white bg-gray-700 hover:bg-gray-800 dark:hover:bg-gray-900 focus:outline-none dark:text-gray-100">
              Create an Employee Account
            </button>
          </div>
<!--          <p class="text-gray-800 text-sm mt-6 text-center dark:text-gray-100">Already have an account?-->
<!--            <RouterLink to="/auth/login" class="text-blue-600 font-semibold hover:underline ml-1 dark:text-gray-100">Login here</RouterLink>-->
<!--          </p>-->
        </form>
      </div>
    </div>
</template>

<style scoped>

</style>
