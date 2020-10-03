<template>
    <AddTodoItem
        @add-todo-item="addTodoItem"
    />
    <select v-model="filter">
        <option>All</option>
        <option>Completed</option>
        <option>Not completed</option>
    </select>
    <br>
    <Loader v-if="loading" />
    <TodoList
        v-else-if="filteredTodos.length"
        v-bind:todos="filteredTodos"
        @change-todo-condition="changeTodoCondition"
        @remove-todo-item="removeTodoItem"
    />
    <p v-else>You don't have any todo yet!</p>

    <div>
        <router-link to="/">Home page</router-link>
    </div>
</template>

<script>
    import TodoList from '@/components/TodoList'
    import AddTodoItem from '@/components/AddTodoItem'
    import Loader from '@/components/Loader'
    export default {
        name: 'App',
        data() {
            return {
                todos: [],
                filter: 'All',
                loading: true
            }
        },
        mounted() {
            fetch('https://jsonplaceholder.typicode.com/todos?_limit=7')
                .then(response => response.json())
                .then(json => {
                    setTimeout(() => {
                        this.todos = json
                        this.loading = false
                    }, 1000)
                })
        },
        components: {
            TodoList,
            AddTodoItem,
            Loader
        },
        methods: {
            changeTodoCondition(id) {
                let reverse_val = !this.todos.find(todo => todo.id === id).completed;
                this.todos.find(todo => todo.id === id).completed = reverse_val;
            },
            removeTodoItem(id) {
                this.todos = this.todos.filter(todo => todo.id !== id)
            },
            addTodoItem(item) {
                this.todos.push(item)
            },
        },
        computed: {
            filteredTodos() {
                let todos = [];

                if (this.filter === 'All') {
                    todos = this.todos
                }
                else if (this.filter === 'Completed') {
                    todos = this.todos.filter(todo => todo.completed === true)
                }
                else if (this.filter === 'Not completed') {
                    todos = this.todos.filter(todo => todo.completed === false)
                }

                return todos;
            }
        }
    }
</script>

<style>
    select {
        font-size: 1.4em;
        margin-bottom: 1em;
    }
</style>