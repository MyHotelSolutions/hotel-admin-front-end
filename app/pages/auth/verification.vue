<template>
    <div class="">
        <Auth>
            <div class="w-2/5 flex flex-col items-center justify-center gap-4">
            <UCard variant="subtle" class="w-100">
                <template #header>
                    <h1 class="font-black uppercase text-base text-center">Verify your email address</h1>
                </template>
    
                <Placeholder class="flex flex-col justify-center items-center gap-2 py-4">
                    <UPinInput length="6"></UPinInput>
                </Placeholder>
                
                <template #footer>
                    <Placeholder class="flex flex-col gap-2">
                        <UButton variant="outline" color="neutral" class="flex flex-col justify-center items-center" size="lg" @click="verification">Verify</UButton>
                        <p class="ml-auto text-xs text-gray-400 hover:text-gray-500 cursor-pointer hover:underline active:underline hover:font-semibold active:font-semibold" @click="resend_verification" v-if="resend_message_visibility">Didn't you get verification code ?</p>
                    </Placeholder>  
                </template>
            </UCard>
        </div>
        </Auth>
    </div>
</template>

<script setup>
import Auth from '~/layouts/auth.vue';

const resend_message_visibility = ref(false)

const verification = () => {
    useRouter().push('/auth/change_password');
}

const resend_verification = () => {
    alert('send verification again')
}

onMounted(() => {
    // verification code send message loaded after 10 of the page loaded 
    setTimeout (() => {
        resend_message_visibility.value = true;

    }, 10000)
})

</script>