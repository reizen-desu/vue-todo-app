<template>
  <div class="container">
    <form class="new-todo-form" @submit.prevent="validateTodo">
      <input type="text" placeholder="Adicione uma nova task" v-model="newTodo" />
      <button type="submit">Add</button>
    </form>
  </div>
</template>

<script>
import { eventBus } from "@/main";

export default {
  name: "new-todo-bar",
  data() {
    return {
      newTodo: "",
    };
  },
  methods: {
    validateTodo() {
      if (this.newTodo.trim().length == 0) {
        alert("Todo is empty");
      } else {
        eventBus.$emit("newTodoInput", this.newTodo);
        this.newTodo = "";
      }
    },
  },
};
</script>

<style lang="css" scoped>
.new-todo-form {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 56px;
}

.new-todo-form input {
  margin-right: 25px;
  padding: 20px 12px;
  border-radius: 12px;
  border: 1px solid #bdbdbd;
  width: 100%;
  font-size: 14px;
}

.new-todo-form button {
  background-color: #2f80ed;
  border: none;
  color: white;
  padding: 20px 40px;
  border-radius: 12px;
}
</style>