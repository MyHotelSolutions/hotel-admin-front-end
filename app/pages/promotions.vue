<template>
    <div class="">
        <Admin>
            <div class="float-right">
                <UModal :ui="{ overlay: 'bg-black/60', content: 'bg-white text-black' }" v-model="popup_status">
                <UButton label="Open" color="neutral" variant="subtle"/>
        
                <template #content>
                    <div class="h-48 m-4">
                    Content here
                    </div>
                </template>
                </UModal>
            </div>
        </Admin>
    </div>
</template>

<script setup lang="ts">
import Admin from '~/layouts/admin.vue';

</script>