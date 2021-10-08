<template>
  <div>
    <div class="cell" v-on:click="onClickSelf">
      <template v-if="a">{{text}}</template>
      <template v-else></template>
    </div>
  </div>
</template>

<script>
export default {
  props: ["n"],
  data() {
    return { a: false, text: "" };
  },

  methods: {
    onClickSelf() {
      if (this.text !== "") {
        return;
      }
      this.a = true;
      this.text = this.n % 2 === 0 ? "x" : "o";
      // $emit告诉相应代码我被点击了
      this.$emit("click", this.text);
    },
  },
};
</script>

<style>
.cell {
  border: 1px solid black;
  width: 200px;
  height: 200px;
  font-size: 125px;
  /* 居中 */
  display: flex;
  justify-content: center;
  align-content: center;
}
</style>