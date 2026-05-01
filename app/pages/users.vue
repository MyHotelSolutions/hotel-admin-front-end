<template>
    <div class="">
        <Admin>
            <div class="flex flex-col gap-8">
                <!-- add new user -->
                <UDrawer direction="right" inset :ui="{ overlay: { background: 'bg-black' } }" overlay-class="bg-black/40">
                    <UButton class="ml-auto w-fit" variant="solid" color="neutral" icon="i-lucide-plus">Add new user</UButton>
                    <template #header>
                        <div class="min-w-96 size-full border-b border-gray-200 py-6">
                            <h1 class="">Add new admin user</h1>
                        </div>
                    </template>
    
                    <template #body>
                        <div class="flex flex-col gap-5 min-w-96 min-h-96 size-full">
                            <UFormField label="First name" required>
                                <UInput placeholder="Nalin" v-model="new_user_details.first_name" class="w-full" :disabled="input_feeld_disabled"/>
                            </UFormField>
                            <UFormField label="Last name" required>
                                <UInput placeholder="Kariyawasam" v-model="new_user_details.last_name" class="w-full" :disabled="input_feeld_disabled"/>
                            </UFormField>
                            <UFormField label="Email" required>
                                <UInput placeholder="nalin.kariyawasam@example.com" v-model="new_user_details.email" class="w-full" :disabled="input_feeld_disabled"/>
                            </UFormField>
                            <UFormField label="Mobile number" required>
                                <UInput placeholder="071 xxx xxxx" v-model="new_user_details.mobile_number" :disabled="input_feeld_disabled"/>
                            </UFormField>
                            <p class="">User Type</p>
                            <URadioGroup v-model="value" :items="items" color="neutral" :disabled="input_feeld_disabled" @change="new_user_details.position = value"/>
                        </div>
                    </template>
                    <template #footer>
                        <div class="min-w-96 size-full border-t border-gray-200 py-4">
                            <UButton @click="addNewUser" variant="solid" color="neutral" :icon="input_feeld_disabled ? 'i-lucide-loader':'i-lucide-plus'" :label=action_lable></UButton>
                        </div>
                    </template>
                </UDrawer>
                
                <!-- show existing users -->
                <div class="">
                    <UTable :data="data" :columns="columns" class="flex-1" />
                </div>
            </div>
            
            <!-- model for block users -->
            <UModal :dismissible="false" title="Block user from admin pannel" v-model:open="open_modal_block" >
                 <template #header/>
                <template #body>
                <Placeholder class="h-48" />
                </template>
            </UModal>

            <!-- model for delete users -->
            <UModal :dismissible="false" title="Remove user from admin pannel" v-model:open="open_modal_delete" >
                 <template #header/>
                <template #body>
                <Placeholder class="h-48" />
                </template>
            </UModal>

            <!-- model for change user's position -->
            <UModal :dismissible="false" title="Change user's position" v-model:open="open_modal_change_position" >
                 <template #header/>
                <template #body>
                <Placeholder class="h-48" />
                </template>
            </UModal>
        </Admin>
    </div>
</template>

<script setup>
definePageMeta({
  layout: 'admin'
})

const items = ref(['Owner', 'Manager', 'Front-desk'])
const value = ref('Owner')
const toast = useToast()
const input_feeld_disabled = ref(false)
const open_modal_block = ref(false)
const open_modal_delete = ref(false)
const open_modal_change_position = ref(false)
const new_user_details = ref({
    'first_name': '',
    'last_name': '',
    'mobile_number': '',
    'email': '',
    'position': items.value[0] 
})
const action_lable = ref('Add User')

watch(
    () => [new_user_details.value.first_name, new_user_details.value.position],
    ([newName, newPosition]) => {
        if (newName === '' ) {
            action_lable.value = `add ${newPosition}`
        }else if (newName !== ''){
            action_lable.value = `add ${newName} as ${newPosition}`
        }
    }
)


const addNewUser = () => {
    input_feeld_disabled.value = true
    console.log("Button clicked!");
    toast.add({
        title: 'Hello world',
        description: 'Testing...',
        icon: 'i-lucide-check',
        color : 'primary', 
    })
}

// table related data
import { h, resolveComponent } from 'vue'
import { useClipboard } from '@vueuse/core'

const UButton = resolveComponent('UButton')
const UDropdownMenu = resolveComponent('UDropdownMenu')

// const toast = useToast()
const { copy } = useClipboard()

// this is for data of the table - user data
const data = ref([
    {
        id: '1',
        first_name: 'Gayashan',
        last_name: 'Gamage',
        email: 'gayashan.gamage@example.com',
        position: 'owner',
        created_at: '2024-03-12T14:30:00',
        last_online: '2024-03-12T16:45:00',
    },
    {
        id: '2',
        first_name: 'James',
        last_name: 'Anderson',
        email: 'james.anderson@example.com',
        position: 'manager',
        created_at: '2024-03-10T10:15:00',
        last_online: '2024-03-13T09:20:00',
    },
    {
        id: '3',
        first_name: 'Sarah',
        last_name: 'Johnson',
        email: 'sarah.johnson@example.com',
        position: 'front-desk',
        created_at: '2024-03-08T08:00:00',
        last_online: '2024-03-13T17:30:00',
    }
])

// this is for column of the table
const columns = [
  {
    accessorKey: 'first_name',
    header: 'First Name',
  },
  {
    accessorKey: 'last_name',
    header: 'Last name',
  },
  {
    accessorKey: 'email',
    header: 'Email'
  },
  {
    accessorKey: 'position',
    header: 'Position',
        
  },
  {
    accessorKey: 'created_at',
    header: 'Created At',
  },
  {
    accessorKey: 'last_online',
    header: 'Last Online',
  },
  {
    id: 'actions',
    meta: {
      class: {
        td: 'text-right'
      }
    },
    cell: ({ row }) => {
      return h(
        UDropdownMenu,
        {
          content: {
            align: 'end'
          },
          items: getRowItems(row),
          'aria-label': 'Actions dropdown'
        },
        () =>
          h(UButton, {
            icon: 'i-lucide-ellipsis-vertical',
            color: 'neutral',
            variant: 'ghost',
            'aria-label': 'Actions dropdown'
          })
      )
    }
  }
]

// this is for action button
function getRowItems() {
  return [
    {
      type: 'label',
      label: 'Actions'
    },
    {
      label: 'View all activities',
    },
    {
      label: 'Change position',
      onSelect(){
          open_modal_change_position.value = true
        }
    },
    {
        label: 'Block user',
        onSelect(){
          open_modal_block.value = true
        }
    },
    {
      label: 'Delete user',
      onSelect(){
          open_modal_delete.value = true
        }
    },
  ]
}

</script>
