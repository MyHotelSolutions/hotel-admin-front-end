<template>
  <!-- outer container -->
  <div
    class="border-10 flex flex-1 w-screen min-h-screen h-full bg-gray-200"
    :class="[
      variant === 'inset' && 'bg-neutral-50 dark:bg-neutral-950',
      side === 'right' && 'flex-row-reverse'
    ]"
  >
    <!-- left sidebar -->
    <USidebar
      v-model:open="open"
      :variant="variant"
      :collapsible="collapsible"
      :side="side"
      :class="open ? 'w-[15%] block' : 'w-[0%] hidden'"
      class="flex flex-col justify-between gap-10 min-h-[calc(100vh-2rem)] py-6 px-4"
    >
    
    <!-- hotel name -->
      <div class="flex flex-row items-center gap-4">
        <div class="bg-gray-400 rounded-full w-12 h-12"></div>
        <div class="flex flex-col">
          <h1 class="font-black text-xl">ABC company</h1>
          <p class="text-sm">Property Manager</p>
        </div>
      </div>

      <!-- sidebar navigation -->
      <UNavigationMenu
        :items="items"
        orientation="vertical"
        class="h-full"
        >
        <template #link="{ items }">
          <NuxtLink
            :to="items.to"
            class="flex items-center gap-2 p-2"
            :class="isActive(items) ? 'bg-gray-300 font-bold' : ''"
          >
            <UIcon :name="items.icon" />
            {{ items.label }}
          </NuxtLink>
        </template>
      </UNavigationMenu>

      <!-- sidebar footer -->
      <div class="">
        <UModal :ui="{ overlay: 'bg-black/60', content: 'bg-white text-black' }" v-model="popup_status">
          <UButton
            icon="i-lucide-log-out"
            color="neutral"
            variant="solid"
            class="float-right py-2 px-6"
            @click="open_popup"
          >
            Logout
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
    </USidebar>

    <!-- right side bar + page content -->
    <div
    class="m-4 rounded-2xl border border-gray-300 flex-1 flex flex-col overflow-hidden lg:peer-data-[variant=floating]:my-4 peer-data-[variant=inset]:m-4 lg:peer-data-[variant=inset]:not-peer-data-[collapsible=offcanvas]:ms-0 peer-data-[variant=inset]:rounded-xl peer-data-[variant=inset]:shadow-sm peer-data-[variant=inset]:ring peer-data-[variant=inset]:ring-default bg-default"
    >
      <!-- this is top bar -->
      <div
        class="h-(--ui-header-height) shrink-0 flex items-center px-4"
        :class="[
          variant !== 'floating' && 'border-b border-default',
          side === 'right' && 'justify-end'
        ]"
      >
        <UButton
          :icon="open ? 'i-lucide-panel-left' : 'i-lucide-panel-right'"
          color="neutral"
          variant="ghost"
          aria-label="Toggle sidebar"
          @click="sidebarToggle()"
        />
      </div>

      <!-- page container -->
      <div class="flex-1 p-4">
        <Placeholder class="size-full">
            <slot></slot>
        </Placeholder>
      </div>
    </div>

    <!-- log out popup -->
    <UModal :ui="{ overlay: 'bg-black/60', content: 'bg-white text-black' }" v-model="popup_status">
        <template #content>
          <div class="h-48 m-4">
            Content here
          </div>
        </template>
      </UModal>
  </div>
</template>

<script setup>
import { link } from '#build/ui'

const open = ref(true)
const route = useRoute()
const popup_status = ref(false);

const items = [
  {
    label: 'Bookings',
    icon: 'lucide:tickets',
    to : '/',
  },
  {
    label: 'Promotions',
    icon: 'lucide:send',
    to : '/promotions',
  },
  {
    label: 'Seervice out',
    icon: 'lucide:flag-off',
    to : '/service_out',
  },
  {
    label: 'Rooms',
    icon: 'lucide:bed-double',
    to : '/rooms',
  },
  {
    label: 'Activities',
    icon: 'lucide:square-chart-gantt',
    to : '/activities',
  },
  {
    label: 'Income Statistics',
    icon: 'lucide:dollar-sign',
    to : '/income_statistics',
  },
  {
    label: 'Site Statistics',
    icon: 'lucide:chart-spline',
    to : '/site_statistics',
  },
  {
    label: 'Users',
    icon: 'lucide:user-round',
    to : '/users',
  },
]

const sidebarToggle = () => {
    open.value = !open.value
}

const isActive = (item) => item.to === route.path

const open_popup = () => {
  popup_status.value = true;
}

</script>