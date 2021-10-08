<template>
  <div class="wrapper">
    <div class="head">
      <p>井字棋</p>
    </div>
    <div class="chess">
      <div class="row">
        <Cell v-on:click="onClickCell(0,$event)" v-bind:n="n" />
        <Cell v-on:click="onClickCell(1,$event)" v-bind:n="n" />
        <Cell v-on:click="onClickCell(2,$event)" v-bind:n="n" />
      </div>
      <div class="row">
        <Cell v-on:click="onClickCell(3,$event)" v-bind:n="n" />
        <Cell v-on:click="onClickCell(4,$event)" v-bind:n="n" />
        <Cell v-on:click="onClickCell(5,$event)" v-bind:n="n" />
      </div>
      <div class="row">
        <Cell v-on:click="onClickCell(6,$event)" v-bind:n="n" />
        <Cell v-on:click="onClickCell(7,$event)" v-bind:n="n" />
        <Cell v-on:click="onClickCell(8,$event)" v-bind:n="n" />
      </div>
      <!-- <div>{{map}}</div> -->
      <div>局势:{{result === null ? '胜负未定' : `已经有胜利者出现 （${result}）` }}</div>

      <div>当前步数:{{n}}</div>
    </div>
  </div>
</template>

<script>
import Cell from "./Cell.vue";
export default {
  components: { Cell },
  data() {
    return {
      n: 0,
      map: [
        [null, null, null],
        [null, null, null],
        [null, null, null],
      ],
      result: null,
    };
  },
  methods: {
    onClickCell(i, text) {
      console.log(`${i},${text}`);
      this.map[Math.floor(i / 3)][i % 3] = text;
      this.n += 1;
      this.tell();
    },
    tell() {
      const map = this.map;
      for (let i = 0; i <= 2; i++) {
        if (
          map[i][0] !== null &&
          map[i][0] === map[i][1] &&
          map[i][1] === map[i][2]
        ) {
          this.result = true;
        }
      }
      for (let j = 0; j <= 2; j++) {
        if (
          map[0][j] !== null &&
          map[0][j] === map[1][j] &&
          map[1][j] === map[2][j]
        ) {
          this.result = true;
        }
      }
      if (
        map[0][0] !== null &&
        map[0][0] === map[1][1] &&
        map[1][1] === map[2][2]
      ) {
        this.result = true;
      }
      if (
        map[0][2] !== null &&
        map[0][2] === map[1][1] &&
        map[1][1] === map[2][0]
      ) {
        this.result = true;
      }
    },
  },
};
</script>

<style>
.wrapper {
  display: flex;
  justify-content: center;
  align-content: center;
}
.head {
  height: 600px;
  width: 600px;
  /* border: 1px solid red; */
  display: flex;
  justify-content: center;
  align-content: center;
  /* flex-direction: column-reverse; */
  /* margin: 0 auto; */
  line-height: 350px;
  font-size: 100px;
  font-weight: bold;
  color: lightblue;
}
.row {
  display: flex;
}
</style>
