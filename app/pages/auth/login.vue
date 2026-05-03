<template>
    <Auth>
        <div class="w-2/5 flex flex-col items-center justify-center gap-4">
            <UCard variant="subtle" class="w-100">
                <template #header>
                    <h1 class="font-black uppercase text-base text-center">Welcome back</h1>
                </template>
    
                <Placeholder class="flex flex-col gap-2 py-4">
                    <UInput type="email" placeholder="Email address" color="neutral" size="lg"></UInput>
                    <UInput type="password" placeholder="Password" color="neutral" size="lg"></UInput>
                </Placeholder>
                
                <template #footer>
                    <Placeholder class="flex flex-col gap-2">
                        <UButton variant="outline" color="neutral" class="flex flex-col justify-center items-center" size="lg" @click="login">Sign In</UButton>
                        <p class="ml-auto text-xs text-gray-400 hover:text-gray-500 cursor-pointer hover:underline active:underline hover:font-semibold active:font-semibold" @click="redirect">Did you forget password ?</p>
                    </Placeholder>  
                </template>
            </UCard>
        </div>
    </Auth>
</template>


<script setup>
import Auth from '~/layouts/auth.vue';

const router = useRouter()

const redirect = () => {
    useRouter().push('/auth/identity');

}

const login = () => {
    router.push('/');
}

</script>