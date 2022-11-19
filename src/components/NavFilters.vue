<template>
  <div class="nav-container">
    <ul>
      <li class="todo-item" :class="{ 'todo-item--active': filterState == 'all' }" @click="updateFilter('all')">
        All
      </li>
      <li class="todo-item" :class="{ 'todo-item--active': filterState == 'active' }" @click="updateFilter('active')">
        Active
      </li>
      <li class="todo-item" :class="{ 'todo-item--active': filterState == 'completed' }"
        @click="updateFilter('completed')">
        Completed
      </li>
    </ul>
    <hr />
  </div>
</template>

<script>
import { eventBus } from "@/main.js";

export default {
  name: "nav-filters",
  data() {
    return {
      filterState: "all",
    };
  },
  methods: {
    updateFilter(newState) {
      this.filterState = newState;
      eventBus.$emit("filterChanged", this.filterState);
    },
  },
};
</script>

<style lang="css" scoped>
ul li {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

ul li:hover {
  color: #2f80ed;
}

.nav-container ul {
  display: flex;
  justify-content: space-around;
}

.nav-container .todo-item {
  font-weight: 600;
  font-size: 14px;
  list-style: none;
  padding: 15px 0px;
  min-width: 90px;
  text-transform: capitalize;
}

.nav-container .todo-item--active {
  color: #2f80ed;
  border-bottom: 4px solid #2f80ed;
}
</style>