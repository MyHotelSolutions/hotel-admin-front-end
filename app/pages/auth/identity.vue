<template>
    <Auth>
        <div class="w-2/5 flex flex-col items-center justify-center gap-4">
            <UCard variant="subtle" class="w-100">
                <template #header>
                    <h1 class="font-black uppercase text-base text-center">Eneter Email</h1>
                </template>
    
                <Placeholder class="flex flex-col gap-2 py-4">
                    <UInput type="email" placeholder="Registered Email" color="neutral" size="lg"></UInput>
                </Placeholder>
                
                <template #footer>
                    <Placeholder class="flex flex-col gap-2">
                        <UButton variant="outline" color="neutral" class="flex flex-col justify-center items-center" size="lg" @click="verify_identity">Verify</UButton>
                    </Placeholder>  
                </template>
            </UCard>
        </div>
    </Auth>
</template>

<script setup lang="ts">
import Auth from '~/layouts/auth.vue';

const verify_identity = () => {
    useRouter().push('/auth/verification');
}

</script>