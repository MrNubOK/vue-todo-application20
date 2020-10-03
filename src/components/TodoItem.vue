<template>
    <li>
        <span>
            <input type="checkbox"
               v-on:change="$emit('change-todo-condition', todo.id)"
            >
            <span v-bind:class="{done: todo.completed}">
                {{ i + 1 }}
                {{ todo.title.toUpperCase() }}
            </span>
        </span>
        <button class="delete-todo"
            v-on:click="$emit('remove-todo-item', todo.id)"
        >&times;</button>
    </li>
</template>

<script>
export default {
    props: {
        todo: {
            type: Object,
            required: true
        },
        i: {
            type: Number
        }
    }
}
</script>

<style scoped>
    li {
        display: flex;
        list-style: none;
        justify-content: space-between;
        padding: 0.7em 1em;
        margin-bottom: 0.7em;
        border: 1px solid rosybrown;
        background: lightsalmon;
        color: white;
        font-weight: 600;
        font-size: 1.4em;
    }

    input[type="checkbox"] {
        margin-right: 1em;
    }

    .delete-todo {
        width: 2em;
        height: 2em;
        border-radius: 50%;
        border: none;
        color: white;
        background: crimson;
    }

    .done {
        text-decoration: line-through;
        color: dimgray;
    }
</style>