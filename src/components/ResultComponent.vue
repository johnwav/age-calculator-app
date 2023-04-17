<script setup>
const props = defineProps(['value'])
</script>

<template>
    <div>
        <div class="result"><span>{{props.value}}</span> <slot></slot></div>
    </div>
</template>

<style scoped>
.result {
    font-size: 100px;
    color: var(--off-black);
}
.result span {
    color: var(--purple);
}
</style>