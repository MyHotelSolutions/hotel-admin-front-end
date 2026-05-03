<template>
  <div class="">
    <Admin>
      <p>booking page</p>
      <UModal :ui="{ overlay: 'bg-black/60', content: 'bg-white text-black' }">
        <UButton label="Open" color="neutral" variant="subtle" />

        <template #content>
          <div class="h-48 m-4">
            Content here
          </div>
        </template>
      </UModal>
    </Admin>
  </div>
</template>

<script setup>
import Admin from '~/layouts/admin.vue';

</script>