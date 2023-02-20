<template>
  <div id="app">
    <TopFont />
    <ContnetHeader :todos="todos" :getTodo="getTodo" :checkAllItem="checkAll" />
    <ContentItem
      v-for="todo in whichTodosShow"
      :key="todo.id"
      :todo="todo"
      :sendCheckedId="changeChecked"
      :getDeleteItem="deleteItem"
    />
    <ContentFooter
      :todos="todos"
      :showWhat="changeShow"
      :showType="whichShow"
    />
  </div>
</template>

<script>
import TopFont from "./components/TopFont.vue";
import ContnetHeader from "./components/ContentHeader.vue";
import ContentItem from "./components/ContentItem.vue";
import ContentFooter from "./components/ContentFooter.vue";

function loadTodosFromLocalStorage() {
  try {
    return JSON.parse(localStorage.todos);
  } catch {
    return [];
  }
}

export default {
  components: {
    TopFont,
    ContnetHeader,
    ContentItem,
    ContentFooter,
  },
  data() {
    return {
      whichShow: "All",
      todos: loadTodosFromLocalStorage(),
    };
  },
  methods: {
    getTodo(todo) {
      this.todos.unshift(todo);
    },
    changeChecked(id) {
      this.todos.forEach(i => {
        if (i.id === id) {
          i.done = !i.done;
        }
      });
    },
    deleteItem(id) {
      this.todos = this.todos.filter(i => i.id !== id);
    },
    changeShow(text) {
      this.whichShow = text;
    },
    checkAll(isAllChecked) {
      this.todos.forEach(i => (i.done = !isAllChecked));
    },
  },
  computed: {
    whichTodosShow() {
      if (this.whichShow === "All") {
        return this.todos;
      } else if (this.whichShow === "Active") {
        return this.todos.filter(i => i.done === false);
      } else if (this.whichShow === "Completed") {
        return this.todos.filter(i => i.done === true);
      }
    },
  },
  watch: {
    todos: {
      deep: true,
      handler(todos) {
        localStorage.todos = JSON.stringify(todos);
      },
    },
  },
};
</script>
<style scoped>
#app {
  width: 500px;
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
}
</style>
