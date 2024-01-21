<template>
  
    <header>

        <h1>{{ title }}</h1>
        <Button @btn-click= "$emit 
        ('show-add-tasks')"  
        :text="showTasks ? 'Close' : 'Add Tasks'" 
        :color= "showTasks ? 'red' : 'green' "/>
    
    </header>

    
</template>

<script>
   
    import Button from './Button.vue'

    export default {

        name: 'Header',

        props: {
            title: String,
            showTasks: Boolean
        },

        components: {
            Button,
        },

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