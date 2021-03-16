<template>
  <v-container>
    <v-row dense v-for="mr in 4" :key="'mr' + mr">
      <v-col v-for="mc in 4" :key="'mc' + mc">
        <v-row no-gutters v-for="r in 10" :key="'r' + r">
          <v-col v-for="c in 26" :key="'c' + c">
            <div
              class="box"
              :class="{ filled: isFilled({ mr, mc, r, c }) }"
            ></div>
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

  isFilled({
    mc,
    mr,
    r,
    c
  }: {
    mc: number;
    mr: number;
    r: number;
    c: number;
  }): boolean {
    const index = c + (r - 1) * 26 + (mc - 1) * 260 + (mr - 1) * 1040;
    return index < this.value;
  }
}
</script>

<style scoped>
.box {
  margin: 1px;
  border-style: solid;
  border-width: 1px;
  border-color: black;
  width: 7px;
  height: 7px;
}

.box.filled {
  background-color: black;
}
</style>
