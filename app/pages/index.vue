<template>
  <div class="">
    <Admin>
      <div class="flex flex-col w-full">

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
            <div class="h-auto m-4">
              
              <!-- header section -->
              <div class="">
                <h3 class="text-lg font-black text-center uppercase">Add new booking</h3>
                <p class="text-sm text-center w-[75%] mx-auto text-gray-400">Lorem ipsum dolor sit amet consectetur adipisicing elit. Perspiciatis, eum.</p>
                <hr class="border-gray-200 my-4">
              </div>

              <!-- body section -->
              <div class="flex flex-col gap-6 justify-center items-center h-[40%]">
                
                <!-- guest informations -->
                <div class="flex flex-col gap-4 w-full">
                  <p class="text-sm text-gray-400 ml-1 font-black">Guest Information</p>
                  <div class="grid grid-cols-2 gap-y-6 gap-x-2 w-full">
                    <UInput placeholder="" :ui="{ base: 'peer'}" class="text-2xl" autocomplete="off" v-model="new_booking.first_name">
                      <label class="pointer-events-none absolute left-0 -top-2.5 text-gray-400 text-xs font-medium px-1.5 transition-all peer-focus:-top-2.5 peer-focus:text-gray-400 peer-focus:text-xs peer-focus:font-medium peer-placeholder-shown:text-sm peer-placeholder-shown:text-dimmed peer-placeholder-shown:top-1.5 peer-placeholder-shown:font-normal">
                        <span class="inline-flex bg-default px-1">First Name</span>
                      </label>
                    </UInput>
                    <UInput placeholder="" :ui="{ base: 'peer' }" v-model="new_booking.last_name">
                      <label class="pointer-events-none absolute left-0 -top-2.5 text-gray-400 text-xs font-medium px-1.5 transition-all peer-focus:-top-2.5 peer-focus:text-gray-400 peer-focus:text-xs peer-focus:font-medium peer-placeholder-shown:text-sm peer-placeholder-shown:text-dimmed peer-placeholder-shown:top-1.5 peer-placeholder-shown:font-normal">
                        <span class="inline-flex bg-default px-1">Last Name</span>
                      </label>
                    </UInput>
                    <UInput placeholder="" :ui="{ base: 'peer' }" type="number" v-model="new_booking.mobile_number">
                      <label class="pointer-events-none absolute left-0 -top-2.5 text-gray-400 text-xs font-medium px-1.5 transition-all peer-focus:-top-2.5 peer-focus:text-gray-400 peer-focus:text-xs peer-focus:font-medium peer-placeholder-shown:text-sm peer-placeholder-shown:text-dimmed peer-placeholder-shown:top-1.5 peer-placeholder-shown:font-normal">
                        <span class="inline-flex bg-default px-1">Mobile Number</span>
                      </label>
                    </UInput>
                    <UInput placeholder="" :ui="{ base: 'peer' }" v-model="new_booking.email">
                      <label class="pointer-events-none absolute left-0 -top-2.5 text-gray-400 text-xs font-medium px-1.5 transition-all peer-focus:-top-2.5 peer-focus:text-gray-400 peer-focus:text-xs peer-focus:font-medium peer-placeholder-shown:text-sm peer-placeholder-shown:text-dimmed peer-placeholder-shown:top-1.5 peer-placeholder-shown:font-normal">
                        <span class="inline-flex bg-default px-1">Email address</span>
                      </label>
                    </UInput>
                  </div>
                </div>

                <hr class="border-gray-300 w-full">

                <!-- booking informations -->
                <div class="flex flex-col gap-4 w-full">
                  <p class="text-sm text-gray-400 ml-1 font-black">Booking Information</p>
                  <div class="grid grid-cols-2 gap-y-6 gap-x-2 w-full">
                    <!-- <UInput :ui="{ base: 'peer'}" class="text-2xl" autocomplete="off" type="date" v-model="check_in_date" min="new Date().toISOString().split('T')[0]" max="">
                      <label class="pointer-events-none absolute left-0 -top-2.5 text-gray-400 text-xs font-medium px-1.5 transition-all peer-focus:-top-2.5 peer-focus:text-gray-400 peer-focus:text-xs peer-focus:font-medium peer-placeholder-shown:text-sm peer-placeholder-shown:text-dimmed peer-placeholder-shown:top-1.5 peer-placeholder-shown:font-normal">
                        <span class="inline-flex bg-default px-1">Check in date</span>
                      </label>
                    </UInput>
                    <UInput placeholder="01/01/2023" :ui="{ base: 'peer' }" type="date" v-model="check_out_date">
                      <label class="pointer-events-none absolute left-0 -top-2.5 text-gray-400 text-xs font-medium px-1.5 transition-all peer-focus:-top-2.5 peer-focus:text-gray-400 peer-focus:text-xs peer-focus:font-medium peer-placeholder-shown:text-sm peer-placeholder-shown:text-dimmed peer-placeholder-shown:top-1.5 peer-placeholder-shown:font-normal">
                        <span class="inline-flex bg-default px-1">Check out date</span>
                      </label>
                    </UInput> -->
                    
                    <UInputDate ref="inputDate" v-model="modelValue">
                      <template #trailing>
                        <UPopover :reference="inputDate?.inputsRef[3]?.$el">
                          <UButton
                            color="neutral"
                            variant="link"
                            size="sm"
                            icon="i-lucide-calendar"
                            aria-label="Select a date"
                            class="px-0"
                          />

                          <template #content>
                            <UCalendar v-model="modelValue" class="p-2" min_value="new Date()"/>
                          </template>
                        </UPopover>
                      </template>
                    </UInputDate>

                    <!-- onboading count -->
                    <div class="flex flex-col gap-2 col-span-2">
                      <div class="flex flex-row justify-between">
                        <p class="text-sm">{{  }}</p>
                        <div class="flex flex-row items-center justify-between gap-4 max-w-[30%]">
                          <UButton size="sm" color="neutral" variant="subtle" @click="adult_count -= 1">-</UButton>
                          <p class="min-w-[3ch] text-center">{{ String(new_booking.adult_count).padStart(2, '0') }}</p>
                          <UButton size="sm" color="neutral" variant="subtle" @click="adult_count += 1">+</UButton>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
                
                <hr class="border-gray-300 w-full">

                <!-- rooms informations -->
                <div class="w-full flex flex-col gap-2 col-span-2">
                  <p class="text-sm text-gray-400 ml-1 font-black">Rooms Information</p>
                  <div class="grid grid-cols-2 gap-2 w-full">
                    <div class="flex flex-row justify-between col-span-2" v-for="items in room_types" :key="items.name">
                      <p class="text-sm">{{ items.name }}</p>
                      <div class="flex flex-row items-center justify-between gap-4 max-w-[30%]">
                        <UButton size="sm" color="neutral" variant="subtle" @click="items.selected_room_count -= 1">-</UButton>
                        <p class="min-w-[3ch] text-center">{{ String(items.selected_room_count).padStart(2, '0') }}</p>
                        <UButton size="sm" color="neutral" variant="subtle" @click="items.selected_room_count += 1">+</UButton>
                      </div>
                    </div>
                  </div>
                </div>
                
                <!-- rooms informations -->
                <div class=""></div>
                
                <!-- price informations -->
                <div class=""></div>

                <!-- <UButton variant="solid" color="neutral" class="h-fit py-2 px-6">Cancel</UButton>
                <UButton variant="solid" color="neutral" class="h-fit py-2 px-6">Logout</UButton> -->
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
  </div>
</template>

<script setup>
import { alert } from '#build/ui';
import Admin from '~/layouts/admin.vue';
import { CalendarDate } from '@internationalized/date'

const inputDate = useTemplateRef('inputDate')

const modelValue = shallowRef(new CalendarDate(2022, 1, 10))

const active = ref('0')
const notconfirm = ref([])
const today = ref([])
const upcomming = ref([])
const compleated = ref([])
const cancelled = ref([])

// booking informations
const min_booking_date = ref('')
const max_booking_date = ref('')
const check_in_date = ref('')
const check_out_date = ref('')
// const max_onboard_guest_count = ref(20)
// const adult_count = ref(2)
// const children_count = ref(0)
const person_count = ref([
  {
    type : 'adult',
    max_count : 20,
    min_count : 1,
  },
  {
    type : 'children',
    max_count : 30,
    min_count : 0,
  }
]) 
const room_types = ref([
  {
    'name': 'room-type-01',
    'max_count': 5,
    'selected_room_count' : 0
  },
  {
    'name': 'room-type-02',
    'max_count': 10,
    'selected_room_count' : 0
  }
])

// this is for the new booking form, which will be used to store the data of the new booking
const new_booking = ref({
  first_name : '',
  last_name : '',
  email : '',
  mobile_number : '',
  check_in_date : '',
  check_out_date : '',
  adult_count : 1,
  children_count : 0,
  room_type_01_count : 1,
  room_type_02_count : 0,
})


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

// set max and min value for the selected rooms in 'room_types'
watch(room_types, (newValue) => {
  if(newValue[0].name == 'room-type-01' && newValue[0].selected_room_count < 0) {
    newValue[0].selected_room_count = 0
  }else if (newValue[0].name == 'room-type-01' && newValue[0].selected_room_count > 5) {
    newValue[0].selected_room_count = 5
  }else if(newValue[1].name == 'room-type-02' && newValue[1].selected_room_count < 0) {
    newValue[1].selected_room_count = 0
  }else if (newValue[1].name == 'room-type-02' && newValue[1].selected_room_count > 10) {
    newValue[1].selected_room_count = 10
  }
},
{
  deep : true
})


onBeforeMount(() => {
  min_booking_date.value = new Date().toISOString().split('T')[0]
  check_in_date.value = new Date().toISOString().split('T')[0]
  check_out_date.value = new Date(Date.now() +259200000).toISOString().split('T')[0]
})

</script>