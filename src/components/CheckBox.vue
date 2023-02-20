<template>
  <div class="box" @click="$emit('toggle')">
    <div :class="{ innerBox: true, checked: checked }"></div>
  </div>
</template>

<script>
export default {
  name: "CheckBox",
  props: ["checked"],
};
</script>

<style lang="less" scoped>
.box {
  width: 20px;
  height: 20px;
  background-color: rgba(241, 190, 250, 0.568);
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
}
.innerBox {
  width: 14px;
  height: 14px;
  border-radius: 50%;
  background-color: white;
}
.checked {
  background-image: radial-gradient(red 20%, white 80%);
}
</style>
