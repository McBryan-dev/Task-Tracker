<template>
  
    <div v-for="task in tasks" :key="task.id">
        <Task @toggle-rem="$emit('toggle-rem', task.id)" @delete-task="$emit('delete-task', task.id) " :task="task"/>
    </div>

</template>

<script>

    import Task from './Task.vue'

    export default {
        name: 'Tasks',
        components: {
            Task
        },
        props: {
            tasks: Array
        },
        emits: ['delete-task', 'toggle-rem']
    }
</script>

<style>

</style>