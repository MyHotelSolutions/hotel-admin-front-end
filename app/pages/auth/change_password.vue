<template>
    <div class="">
        <Auth>
            <div class="w-2/5 flex flex-col items-center justify-center gap-4">
            <UCard variant="subtle" class="w-100">
                <template #header>
                    <h1 class="font-black uppercase text-2xl text-center">Change password</h1>
                </template>
    
                <Placeholder class="flex flex-col justify-center items-center gap-2 py-4">
                    <UInput type="password" placeholder="Password" color="neutral" size="lg" class="w-full" v-model="password"></UInput>
                    <UInput type="password" placeholder="Repeat Password" color="neutral" size="lg" class="w-full" v-model="repeat_password"></UInput>
                </Placeholder>
                
                <template #footer>
                    <Placeholder class="flex flex-col gap-6">
                        <UButton variant="outline" color="neutral" :disabled="password_change_button" class="flex flex-col justify-center items-center" size="lg" @click="change_password">Confirm</UButton>
                        
                        <!-- check password indicator -->
                        <div class="">
                            <!-- passwords are mached or not -->
                            <div class="flex flex-row gap-5 items-center">
                                <LucideSquareCheckBig class="text-green-500" v-if="mached"></LucideSquareCheckBig>
                                <LucideSquareX class="text-red-500" v-else="mached"></LucideSquareX>
                                <p class="text-sm" :class="mached == true ? 'text-green-500' : 'text-red-500'">{{ mached ? 'Passwords match' : 'Passwords do not match' }}</p>
                            </div>
                            <!-- lenght of the password -->
                            <div class="flex flex-row gap-5 items-center">
                                <LucideSquareCheckBig class="text-green-500" v-if="lenght"></LucideSquareCheckBig>
                                <LucideSquareX class="text-red-500" v-else="lenght"></LucideSquareX>
                                <p class="text-sm" :class="lenght == true ? 'text-green-500' : 'text-red-500'">Lenght should be at least 8 characters</p>
                            </div>
                            <!-- lenght of the password -->
                            <div class="flex flex-row gap-5 items-center">
                                <LucideSquareCheckBig class="text-green-500" v-if="uppercase"></LucideSquareCheckBig>
                                <LucideSquareX class="text-red-500" v-else="uppercase"></LucideSquareX>
                                <p class="text-sm" :class="uppercase == true ? 'text-green-500' : 'text-red-500'">Should include at leased 2 uppercase letters</p>
                            </div>
                            <!-- lenght of the password -->
                            <div class="flex flex-row gap-5 items-center">
                                <LucideSquareCheckBig class="text-green-500" v-if="lowercase"></LucideSquareCheckBig>
                                <LucideSquareX class="text-red-500" v-else="lowercase"></LucideSquareX>
                                <p class="text-sm" :class="lowercase == true ? 'text-green-500' : 'text-red-500'">Should include at leased 2 lowercase letters</p>
                            </div>
                            <!-- lenght of the password -->
                            <div class="flex flex-row gap-5 items-center">
                                <LucideSquareCheckBig class="text-green-500" v-if="number"></LucideSquareCheckBig>
                                <LucideSquareX class="text-red-500" v-else="number"></LucideSquareX>
                                <p class="text-sm" :class="number == true ? 'text-green-500' : 'text-red-500'">Should include at least 2 numbers</p>
                            </div>
                            <!-- lenght of the password -->
                            <div class="flex flex-row gap-5 items-center">
                                <LucideSquareCheckBig class="text-green-500" v-if="special"></LucideSquareCheckBig>
                                <LucideSquareX class="text-red-500" v-else="special"></LucideSquareX>
                                <p class="text-sm" :class="special == true ? 'text-green-500' : 'text-red-500'">Should include at least 1 special characters</p>
                            </div>
                        </div>
                    
                    </Placeholder>  
                </template>
            </UCard>
        </div>
        </Auth>
    </div>
</template>

<script setup>
import Auth from '~/layouts/auth.vue';

const mached = ref(false)
const lenght = ref(false);
const uppercase = ref(false);
const lowercase = ref(false);
const number = ref(false);
const special = ref(false);
const password_change_button = ref(true)
const password = ref('');
const repeat_password = ref('');

const change_password = () => {
    useRouter().push('/auth/login');
}

watch(password, (newPassword, oldPassword) => {
    uppercase.value = (newPassword.match(/[A-Z]/g) || []).length >= 2;
    lowercase.value = (newPassword.match(/[a-z]/g) || []).length >= 2;
    number.value = (newPassword.match(/[0-9]/g) || []).length >= 2;
    special.value = (newPassword.match(/[@$!%*?&]/g) || []).length >= 1;
    lenght.value = newPassword.length >= 8;
})

watch([password, repeat_password], ([newPassword, newRepeatPassword]) => {
    if(
        lenght.value == true &&
        uppercase.value == true &&
        lowercase.value == true &&
        number.value == true &&
        special.value == true && 
        newPassword === newRepeatPassword
    ){
        mached.value = true
        password_change_button.value = false
    }else{
        mached.value = false
        password_change_button.value = true
    }
})

</script>