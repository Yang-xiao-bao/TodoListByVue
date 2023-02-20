<template>
  <div>
    <div class="container">
      <label @click="allCheck" :class="allCheckedClass">
        <DownOutlined />
      </label>
      <input
        type="text"
        v-model="msg"
        @keyup.enter="keyUpEnter"
        placeholder="What needs to be done?"
        class="input"
      />
    </div>
  </div>
</template>

<script>
import { DownOutlined } from "@ant-design/icons-vue";
import { nanoid } from "nanoid";
export default {
  name: "ContnetHeader",
  components: { DownOutlined },
  props: ["getTodo", "todos", "checkAllItem"],
  data() {
    return {
      msg: "",
      class: "icon",
    };
  },
  methods: {
    keyUpEnter(e) {
      const todo = {
        id: nanoid(),
        msg: this.msg,
        done: false,
      };
      this.getTodo(todo);
      this.msg = "";
    },
    allCheck() {
      this.checkAllItem(this.isAllChecked);
    },
  },
  computed: {
    isAllChecked() {
      return this.todos.every(i => i.done);
    },
    allCheckedClass() {
      if (this.isAllChecked) {
        return "icon allCheck";
      } else {
        return "icon";
      }
    },
  },
};
</script>

<style scope>
.container {
  display: flex;
  align-items: center;
  padding: 16px 16px 16px 16px;
  border: 1px solid #ccc;
}
.input {
  width: 80%;
  height: 32px;
  font-size: 24px;
  color: rgb(126, 126, 126);
  flex: 1;
  border: none;
  outline: none;
}
.icon {
  width: 40px;
  color: rgb(126, 126, 126);
}
.allCheck {
  color: red;
}
</style>
