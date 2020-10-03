<template>
    <ul>
        <TodoItem
            v-for="(todo, i) of todos" :key="todo.id"
            v-bind:todo="todo"
            v-bind:i="i"
            @change-todo-condition="changeTodoCondition"
            @remove-todo-item="removeTodoItem"
        />
    </ul>
</template>

<script>
import TodoItem from '@/components/TodoItem'
export default {
    props: ['todos'],
    components: {
        TodoItem
    },
    methods: {
        changeTodoCondition(id) {
            this.$emit('change-todo-condition', id)
        },
        removeTodoItem(id) {
            this.$emit('remove-todo-item', id)
        }
    }
}
</script>

<style>
    ul {
        padding: 0;
        margin: 0;
    }
</style>