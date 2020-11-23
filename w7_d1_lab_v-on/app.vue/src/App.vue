<template>
    <div id="app">
        <form v-on:submit.prevent="updateToDo">
            <label for="new-to-do">Create a To Do List</label>
            <input type="text" id="new-to-do" v-model="newToDo">
            <input type="submit" value="Add Item to List">
        </form> 

        <ul>
            <li v-for="(todo,index) in todos" v-bind:key="index">
                <span>{{todo.name}}</span>
                <!-- <span for if high / low priority> -->
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    data() {
        return {
            todos: [
                {name: 'Buy shopping', priority: "high"},
                {name: 'Clean bathroom', priority: "high"},
                {name: 'Service bike', priority: "low"}
            ],
        newToDo: ""
        }
    },
    methods: {
        updateToDo: function() {
            this.todos.push(this.newToDo);
        this.newToDo = "";
        }
    }
}

</script>

<style>

</style>