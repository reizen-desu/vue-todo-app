<template>
  <div class="todo-list-container">
    <ul class="todo-list">
      <li v-for="(todo, index) in filteredTodos" :key="index" class="todo-item">
        <div>
          <input type="checkbox" :checked="todo.completed" v-model="todo.completed" />
          <label :class="{ completed: todo.completed }">{{ todo.title }}</label>
        </div>
        <button v-if="filter == 'completed'" class="delete-btn" @click="deleteTodo(index)">
          <span class="delete-icon material-icons-outlined"> delete </span>
        </button>
      </li>
    </ul>
    <div class="delete-all-container">
      <button @click="deleteAllCompleted" v-if="filter == 'completed'" class="delete-all-btn">
        <span class="delete-all__icon material-icons-outlined"> delete </span>
        <span class="delete-all__text">delete all</span>
      </button>
    </div>
  </div>
</template>

<script>
import { eventBus } from "@/main";

export default {
  name: "todo-list",
  props: {},
  data() {
    return {
      filter: "all",
      nextTodoId: 0,
      todoItems: [],
    };
  },
  created() {
    eventBus.$on("newTodoInput", (newTodo) => this.createTodo(newTodo));
    eventBus.$on("filterChanged", (newFilter) => (this.filter = newFilter));
  },
  methods: {
    createTodo(newTodoTitle) {
      this.todoItems.push({
        id: this.nextTodoId,
        title: newTodoTitle,
        completed: false,
      });
      this.nextTodoId++;
    },
    deleteTodo(index) {
      this.todoItems.splice(index, 1);
    },
    deleteAllCompleted() {
      this.todoItems = this.todoItems.filter((todo) => !todo.completed);
    },
  },
  computed: {
    filteredTodos() {
      let filteredArray;

      if (this.filter == "active") {
        filteredArray = this.todoItems.filter((todo) => !todo.completed);
      } else if (this.filter == "completed") {
        filteredArray = this.todoItems.filter((todo) => todo.completed);
      } else {
        filteredArray = this.todoItems;
      }

      return filteredArray;
    },
  },
};
</script>

<style scoped lang="css">
.todo-list-container .todo-list {
  display: grid;
  grid-row-gap: 22px;
}

.todo-list-container .completed {
  text-decoration: line-through;
}

.todo-list-container .todo-item {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.todo-list-container .todo-item div {
  display: flex;
  align-items: center;
}

.todo-list-container .todo-item div input[type="checkbox"] {
  height: 18px;
  width: auto;
}

.todo-list-container .todo-item div label {
  margin-left: 7px;
  font-size: 18px;
}

.todo-list-container .todo-item .delete-btn {
  background-color: transparent;
  border: none;
}

.todo-list-container .todo-item .delete-btn .delete-icon {
  font-size: 18px;
  color: #bdbdbd;
}

.todo-list-container .delete-all-container {
  margin-top: 33px;
  display: flex;
  justify-content: flex-end;
}

.todo-list-container .delete-all-container .delete-all-btn {
  background-color: #eb5757;
  display: flex;
  align-items: center;
  justify-content: center;
  border: none;
  color: white;
  padding: 12px 30px;
  border-radius: 4px;
  font-size: 12px;
}

.todo-list-container .delete-all-container .delete-all__icon {
  font-size: 10px;
  margin-right: 5px;
}
</style>
