<template>
    <div v-if="tasks.length">
        <div v-for="task in tasks" v-bind:key="task.id">
            <Task v-bind:task="task" @delete-task="deleteTask" @dblclick="$emit('toggle-reminder',task.id)" />
        </div>
    </div>
        <Alert v-else :message="'No task has been added yet'" />
</template>

<script>
import Task from './Task.vue';
import Alert from './Alert.vue';
export default {
    name: "Tasks",
    props: {
        tasks: Array
    },
    components: { Task, Alert },
    methods: {
        deleteTask(id){
            this.$emit('delete-task',id);
        }
    }
}
</script>

