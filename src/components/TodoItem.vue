<template>
  <div class="container">
    <div class="row">
      <div class="px-2 py-2" v-bind:class="{'is-complete': todo.completed}">
        <p class="px-3">
          <input type="checkbox" v-on:change="markComplete" />
          {{todo.title}}
        </p>
        <button @click="$emit('del-todo', todo.id)" class="btn btn-danger">delete</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    markComplete() {
      this.todo.completed = !this.todo.completed;
    }
  }
};
</script>

<style scoped>
.todo-item {
  background: #f4f4f4;
  padding: 10px;
  border-bottom: 1px #ccc dotted;
}

.is-complete {
  text-decoration: line-through;
}

.del {
  background: #ff0000;
  color: #fff;
}
</style>