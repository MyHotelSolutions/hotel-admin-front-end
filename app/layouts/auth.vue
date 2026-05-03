<template>
    <div class="w-full h-screen flex flex-row items-center justify-center">
        
        <div class="w-3/5 h-full">
            <img src="https://ik.imagekit.io/myHotelSolutions/h-admin/un-organized/paris.jpg" alt="" class="w-full h-full object-cover" />
        </div>

        <div class="w-2/5 flex flex-col items-center justify-center gap-4">
            <slot></slot>
        </div>
    </div>
</template>

<script setup></script>