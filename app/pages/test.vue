<template>
    <div class="">
        <UModal
            title="Modal with close button"
            v-model:open="modal"
            
          >
          
          <template #body>
              <Placeholder class="h-48" />
            </template>
        </UModal>
        <UButton label="Open" color="neutral" variant="subtle" @click="modal=true"/>
    </div>
</template>

<script setup>
const modal = ref(null)
</script>