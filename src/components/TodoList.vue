<template>
    <div class="container">
        <h1>To Do List</h1>
        <div v-if="!isEdting">
            <input type="text" v-model="todo">
            <input type="submit" value="add" @click="storeTodo" :disabled="!todo">
        </div>
        <div v-else>
            <input type="text" v-model="todo">
            <input type="submit" value="update" @click="updateTodo">
        </div>
        <ol>
            <li v-for="(todo, index) in todos" :key="index">
            {{ todo }}
            <button @click="editTodo(index, todo)">Edit</button> 
            <button @click="deleteTodo(index)">Delete</button>
            </li>
        </ol>
    </div>
</template>

<script>
export default {
    name: 'ToDoList',
    data() {
        return {
            isEdting: false,
            selectedIndex: null,
            todo: '',
            todos: []
        };
    },
    methods: {
        storeTodo() {
            this.todos.push(this.todo);
            this.todo = ''
        },
        editTodo(index, todo) {
            this.todo = todo;
            this.selectedIndex = index;
            this.isEdting = true;
        },
        updateTodo() {
            this.todos.splice(this.selectedIndex, 1, this.todo);
            this.todo = '';
            this.isEdting = false;
        },
        deleteTodo(index) {
            this.todos.splice(index, 1);
        }
    }
}
</script>

<style>
    body {
        background-color: rgb(173, 129, 223);
        color: antiquewhite;
        font-family: 'Courier New', Courier, monospace;
    }
    .container {
        text-align: left;
        color: rgb(0, 25, 58);
    }
    h1 {
        padding-top: 40px;
        }
    button{
        margin-left: 12px;
    }
</style>