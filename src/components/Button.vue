<template>
    <button @click="$emit('btn-click')" :style="{background: color}" class="btn">{{ text }}</button>
</template>

<script>
    export default {
        name: 'Button',
        props: {
            text: String,
            color: String,
        }
    }
</script>

<style scoped>
button {
    padding: .375rem .75rem;
    width: 6rem;
    height: fit-content;
    font-weight: bold;
}
</style>