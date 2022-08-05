<template>
    <div class="alert">
        <p>{{message}}</p>
    </div>
</template>

<script>
    export default {
        name: "Alert",
        props: {
            message: String
        }
    }
</script>

<style scoped>

    .alert{
        background: red;
        text-align: center;
        color: white;
        padding: .375rem 0;
        border-radius: .25rem;
            user-select: none;
        }
</style>