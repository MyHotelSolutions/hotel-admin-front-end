<template>
  <!-- outer container -->
  <div
    class="border-10 flex flex-1 w-screen min-h-screen h-full"
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
    >
    
    <!-- hotel name -->
      <div class="">
        <h1 class="font-black text-2xl text-center py-6">ABC admin</h1>
      </div>

      <!-- sidebar navigation -->
      <UNavigationMenu
        :items="items"
        orientation="vertical"
        :ui="{ link: 'p-1.5 overflow-hidden' }"
      />
    </USidebar>

    <!-- right side bar -->
    <div
    class="m-4 rounded-2xl border flex-1 flex flex-col overflow-hidden lg:peer-data-[variant=floating]:my-4 peer-data-[variant=inset]:m-4 lg:peer-data-[variant=inset]:not-peer-data-[collapsible=offcanvas]:ms-0 peer-data-[variant=inset]:rounded-xl peer-data-[variant=inset]:shadow-sm peer-data-[variant=inset]:ring peer-data-[variant=inset]:ring-default bg-default"
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
      <div class="flex-1 p-4 border-4 border-amber-300">
        <Placeholder class="size-full">
            <slot></slot>
        </Placeholder>
      </div>
    </div>
  </div>
</template>

<script setup>
import { alert } from '#build/ui';

const open = ref(true)

const items = [
  {
    label: 'Home',
    icon: 'lucide:circle-user',
    active: false
  },
]

const sidebarToggle = () => {
    open.value = !open.value
}

</script>