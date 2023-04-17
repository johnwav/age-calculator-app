<script setup>

const props = defineProps(['for'])

</script>

<template>
    <div class="date">
        <label :for="props.for">
            <slot></slot>
        </label>
        <input @keyup.enter="submit" type="text" @change="$emit('saveInput', $event.target.value)" :name="props.for" />
    </div>
</template>


<style scoped> .date {
     display: flex;
     flex-direction: column;
     gap: 8px;
 }

 input {
     width: 160px;
     font-size: var(--inputsize);
     color: var(--smokey-grey);
     border: 1px solid var(--light-grey);
     border-radius: 8px;
     height: 70px;
     color: var(--off-black);
     padding-inline: 24px;
 }

 label {
     color: var(--smokey-grey);
     font-size: 15px;
     letter-spacing: 5px;

 }
</style>