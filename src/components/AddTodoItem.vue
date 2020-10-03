<template>
    <form class="add-item-form" v-on:submit.prevent="addTodoItem">
        <input class="add-item-text" type="text" placeholder="Enter text" v-model="title">
        <input class="add-item-button" type="submit" value="Add new">
    </form>
</template>

<script>
export default {
    data() {
      return {
          title: ''
      }
    },
    methods: {
        addTodoItem() {
            let new_item = {
              id: Date.now(),
              title: this.title,
              completed: false
            };

            this.$emit('add-todo-item', new_item)
            this.title = ''
        }
    }
}
</script>

<style>
    .add-item-form {
        display: flex;
        justify-content: space-between;
        margin-bottom: 1em;
    }

    .add-item-text {
        padding: 0.2em 0.4em;
        font-size: 1.4em;
        float: left;
        width: 70%;
    }

    .add-item-button {
        float: right;
    }
</style>

