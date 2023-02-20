<template>
  <div>
    <div class="container">
      <CheckBox @toggle="changeCheck" :checked="todo.done" />
      <div :class="msgClass">{{ todo.msg }}</div>
      <div class="delete" @click="deleteItem(todo.id)">
        <CloseOutlined />
      </div>
    </div>
  </div>
</template>

<script>
import { CloseOutlined } from "@ant-design/icons-vue";
import CheckBox from "./CheckBox.vue";
export default {
  name: "ContentItem",
  components: { CloseOutlined, CheckBox },
  props: ["todo", "sendCheckedId", "getDeleteItem"],
  computed: {
    msgClass() {
      if (this.todo.done) {
        return `todo done`;
      } else {
        return "todo";
      }
    },
  },
  methods: {
    changeCheck() {
      this.sendCheckedId(this.todo.id);
    },
    deleteItem(id) {
      this.getDeleteItem(id);
    },
  },
};
</script>

<style lang="less" scoped>
.container {
  padding: 16px;
  display: flex;
  align-items: center;
}
.checkbox {
  width: 40px;
  input {
    transform: scale(0.8);
  }
  input:checked:before {
    background-color: green;
  }
}
// .checkbox input {
//   font-size: 40px;
// }
.todo {
  flex: 1;
  font-size: 24px;
  color: rgb(105, 105, 105);
  margin-left: 20px;
}
.done {
  color: rgb(190, 190, 190);
  text-decoration: line-through;
}
.delete {
  width: 40px;
  display: none;
}
.container:hover .delete {
  display: block;
}
</style>
