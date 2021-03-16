<template>
  <v-container>
    <v-row>
      <v-col v-for="m in 16" :key="'m' + m" sm="6" lg="3" cols="12">
        <v-row no-gutters v-for="r in 10" :key="'r' + r">
          <v-col
            v-for="c in 26"
            :key="'c' + c"
            class="box"
            :class="{ filled: isFilled({ m, r, c }) }"
          >
          </v-col>
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class HelloWorld extends Vue {
  @Prop() private value!: number;

  isFilled({ m, r, c }: { m: number; r: number; c: number }): boolean {
    const index = c + (r - 1) * 26 + (m - 1) * 260;
    return index < this.value;
  }
}
</script>

<style scoped>
.box {
  margin: 2px;
  border-style: solid;
  border-width: 1px;
  border-color: grey;
  height: 13px;
}

.box.filled {
  background-color: black;
}
</style>
