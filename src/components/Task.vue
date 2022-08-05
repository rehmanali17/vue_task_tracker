<template>
    <div class="task-container" v-bind:class="task.reminder && 'reminder'">
        <div class="task">
            <h3>
                {{task.text}}
            </h3>
            <div>
                <!-- <i @click="$emit('edit-task',task.id)" class="icon-btn">&vellip;</i> -->
                <i @click="deleteTask(task.id)" class="icon-btn delete">&times;</i>
            </div>
        </div>
        <p>{{task.day}}</p>
    </div>
</template>

<script>
    export default {
        name: "Task",
        props: ['task'],
        methods: {
            deleteTask(id){
                this.$emit('delete-task',id)
            }
        }
    }
</script>

<style scoped>
.icon-btn {
    font-size: 2rem;
    cursor: pointer;
    font-weight: bold;
    margin: 0 .5rem;
}
.icon-btn:active {
    transform: translate(0.95);
}

.icon-btn.delete{
    color: red;
}

.task-container {
    background: #f4f4f4;
    margin: 5px;
    padding: 10px 20px;
    cursor: pointer;
}

.task-container.reminder {
    border-left: 5px solid green;
}

.task{
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.task h3 {
    display: flex;
    align-items: center;
    justify-content: space-between;
}
</style>