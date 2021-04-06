<template>
  <v-container>
    <v-row no-gutters v-for="r in 40" :key="'r' + r">
      <v-col v-for="c in 104" :key="'c' + c" class="box-container">
        <div class="stretch"></div>
        <div class="box" />
        <div
          class="box filled"
          v-if="isFilled({ r, c })"
          :class="{ current: isCurrent({ r, c }) }"
        ></div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import anime from "animejs";

@Component
export default class HelloWorld extends Vue {
  @Prop() private value!: number;

  isFilled({ r, c }: { r: number; c: number }): boolean {
    return this.getIndex({ r, c }) <= this.value;
  }
  isCurrent({ r, c }: { r: number; c: number }): boolean {
    return this.getIndex({ r, c }) == this.value;
  }

  getIndex({ r, c }: { r: number; c: number }): number {
    return c + (r - 1) * 104;
  }

  mounted() {
    this.animate();
  }
  animate() {
    anime
      .timeline()
      .add({
        targets: ".box.filled",
        scale: [
          { value: 0, duration: 0 },
          { value: 1, easing: "easeInOutQuad", duration: 900 }
        ],
        delay: anime.stagger(40, { grid: [104, 40], from: 0 })
      })
      .add({
        targets: ".box.filled.current",
        scale: [
          { value: 0, duration: 50 },
          { value: 1, easing: "easeInOutQuad", duration: 50 }
        ]
      });
  }
}
</script>

<style scoped>
.box-container {
  display: inline-block;
  position: relative;
}

.stretch {
  margin-top: 100%;
}

.box {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: #00d672;
  opacity: 0.1;
  margin: 2px;
}
.box.filled.current {
  background-color: rgb(148, 3, 129);
}
.box.filled {
  opacity: 1;
}
</style>
