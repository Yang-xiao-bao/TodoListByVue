<template>
  <div>
    <div id="container">
      <div class="msg">{{ doneItems }} items left</div>
      <button
        class="btn"
        :class="showType === 'All' ? 'btnHigtLight' : ''"
        v-on:click="whichShow"
      >
        All
      </button>
      <button
        class="btn"
        :class="showType === 'Active' ? 'btnHigtLight' : ''"
        @click="whichShow"
      >
        Active
      </button>
      <button
        class="btn"
        :class="showType === 'Completed' ? 'btnHigtLight' : ''"
        @click="whichShow"
      >
        Completed
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "ContentFooter",
  props: ["todos", "showWhat", "showType"],
  computed: {
    doneItems() {
      return this.todos.filter(i => i.done).length;
    },
  },
  methods: {
    whichShow(e) {
      console.log("function");
      this.showWhat(e.target.innerText);
    },
  },
};
</script>

<style lang="less" scoped>
#container {
  height: 20px;
  padding: 16px 16px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  border: 1px solid #ccc;
  position: relative;
}
#container::before {
  content: "";
  position: absolute;
  right: 0;
  bottom: 0;
  left: 0;
  height: 50px;
  overflow: hidden;
  box-shadow: 0 1px 1px rgb(0 0 0 / 20%), 0 8px 0 -3px #f6f6f6,
    0 9px 1px -3px rgb(0 0 0 / 20%), 0 16px 0 -6px #f6f6f6,
    0 17px 2px -6px rgb(0 0 0 / 20%);
  pointer-events: none;
}
.msg {
  margin-right: 50px;
}
.btn {
  background-color: white;
  padding: 0px 30px;
  border: 0.5px solid #ccc;
  border-radius: 6px;
}
.btn:hover {
  border: 0.5px solid rgba(241, 190, 250, 0.568);
}
.btnHigtLight {
  background-color: rgba(241, 190, 250, 0.568);
}
</style>
