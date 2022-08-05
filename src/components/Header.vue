<template>
    <header>
        <h1>{{name}}</h1>
        <Button @btn-click="$emit('btn-click')" :text="showAddTask ? 'Close' : 'Add Task'"
            :color="showAddTask ? 'red' : 'black'" />
    </header>
</template>

<script>
import Button from './Button.vue'
export default {
    name: "Header",
    props: {
        name: String,
        showAddTask: Boolean
    },
    components: { Button }
}
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>