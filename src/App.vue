<template>
  <div id="app">
    <div class="container">
      <h1 class="page-title">#todo</h1>
      <nav-filters></nav-filters>
      <new-todo-bar v-if="filter != 'completed'"></new-todo-bar>
      <todo-list></todo-list>
      <footer>
        <p>Reizen dos Santos</p>
      </footer>
    </div>
  </div>
</template>

<script>
import NavFilters from "@/components/NavFilters";
import NewTodoBar from '@/components/NewTodoBar'
import TodoList from '@/components/TodoList'
import { eventBus } from '@/main'

export default {
  name: "App",
  components: {
    NavFilters,
    NewTodoBar,
    TodoList,
  },
  data() {
    return {
      filter: 'all'
    }
  },
  created() {
    eventBus.$on('filterChanged', (newFilter) => this.filter = newFilter)
  }
};
</script>

<style lang="css">
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

#app {
  display: flex;
  justify-content: center;
  margin-top: 30px;
}

#app .container {
  width: 600px;
  text-align: center;
  display: grid;
  grid-row-gap: 10px;
}

.page-title {
  font-weight: 700;
  font-size: 36px;
  color: gray;
}

footer {
  margin-top: 300px;
  padding: 20px;
  color: gray;
  text-shadow: 0px 0px 1px #000000;
}

footer p {
  color: #a9a9a9;
}
</style>
