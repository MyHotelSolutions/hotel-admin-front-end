<template>
  <Admin>
    <div class="flex flex-col w-full">
      <!-- button bar ( tabs list and 'new booking' button ) -->
      <div class="flex flex-row justify-between">
        
        <!-- tab options list -->
        <UTabs
        :items="items"
        orientation="horizontal"
        class="w-[60%]"
        variant="pill"
        color="neutral"
        v-model="active"
        />

        <!-- add new booking popup -->
        <UModal :ui="{ overlay: 'bg-black/60', content: 'bg-white text-black' }" v-model="popup_status">
          <UButton
            icon="i-lucide-plus"
            color="neutral"
            variant="solid"
            class="float-right py-2 px-6 h-fit"
            @click="open_popup"
          >
            Add New Booking
          </UButton>

          <template #content>
            <div class="h-44 m-4">
              
              <!-- header section -->
              <div class="">
                <h3 class="text-lg font-black text-center uppercase">Logout</h3>
                <p class="text-sm text-center w-[75%] mx-auto text-gray-400">This action will log you out of the system. cannot do any task on the system.</p>
                <hr class="border-gray-200 my-4">
              </div>

              <!-- body section -->
              <div class="flex flex-row gap-2 justify-center items-center h-[40%]">
                <UButton variant="solid" color="neutral" class="h-fit py-2 px-6">Cancel</UButton>
                <UButton variant="solid" color="neutral" class="h-fit py-2 px-6">Logout</UButton>
              </div>
            </div>
          </template>
        </UModal>
      </div>

      <!-- table content -->
      <div class="">
        <UTable :data="data" class="flex-1" />
      </div>

    </div>
  </Admin>
</template>

<script setup>
import Admin from '~/layouts/admin.vue'

const active = ref('0')
const notconfirm = ref([])
const today = ref([])
const upcomming = ref([])
const compleated = ref([])
const cancelled = ref([])

const items = [
  { label: 'Not confirmed  02', icon: 'i-lucide-folder-clock', value: '0' },  
  { label: 'Today 03', icon: 'i-lucide-folder-clock', value: '1' },
  { label: 'Upcomming 06', icon: 'i-lucide-folder-up', value: '2' },
  { label: 'Compleated', icon: 'i-lucide-folder-down', value: '3' },
  { label: 'Cancelled', icon: 'i-lucide-folder-x', value: '4' }
]

const data = ref([
  {
    id: '4600',
    date: '2024-03-11T15:30:00',
    status: 'paid',
    email: 'james.anderson@example.com',
    amount: 594
  },
  {
    id: '4599',
    date: '2024-03-11T10:10:00',
    status: 'failed',
    email: 'mia.white@example.com',
    amount: 276
  },
  {
    id: '4598',
    date: '2024-03-11T08:50:00',
    status: 'refunded',
    email: 'william.brown@example.com',
    amount: 315
  },
  {
    id: '4597',
    date: '2024-03-10T19:45:00',
    status: 'paid',
    email: 'emma.davis@example.com',
    amount: 529
  },
  {
    id: '4596',
    date: '2024-03-10T15:55:00',
    status: 'paid',
    email: 'ethan.harris@example.com',
    amount: 639
  }
])
</script>