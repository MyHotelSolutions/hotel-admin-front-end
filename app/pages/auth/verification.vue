<template>
    <div class="">
        <Auth>
            <div class="w-2/5 flex flex-col items-center justify-center gap-4">
            <UCard variant="subtle" class="w-100">
                <template #header>
                    <h1 class="font-black uppercase text-2xl text-center">Verify your email address</h1>
                </template>
    
                <Placeholder class="flex flex-col justify-center items-center gap-2 py-4">
                    <UPinInput length="6"></UPinInput>
                </Placeholder>
                
                <template #footer>
                    <Placeholder class="flex flex-col gap-2">
                        <UButton variant="outline" color="neutral" class="flex flex-col justify-center items-center" size="lg" @click="verification">Verify</UButton>
                    </Placeholder>  
                </template>
            </UCard>
        </div>
        </Auth>
    </div>
</template>

<script setup>
import Auth from '~/layouts/auth.vue';

const verification = () => {
    useRouter().push('/auth/change_password');
}
</script>