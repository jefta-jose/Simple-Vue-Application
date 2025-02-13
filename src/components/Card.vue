<script setup>

const props = defineProps({
    bg:{
        type: String,
        default: 'background-color: rgba(128, 128, 128, 0.505);'
    }
});

</script>

<template>
    <div :style="bg">
        <slot></slot>
    </div>
</template>

<style scoped>
*{
    border-radius: 8px;
}
</style>