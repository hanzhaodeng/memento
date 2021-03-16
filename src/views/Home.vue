<template>
  <div>
    <v-row>
      <v-col>
        <h1 class="title">Memento Mori</h1>
      </v-col>
    </v-row>
    <Mori value="10" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Mori from "@/components/Mori.vue";

@Component({
  components: {
    Mori
  }
})
export default class Home extends Vue {}
</script>

<style scoped>
.title {
  text-align: center;
  font-weight: bold;
  font-size: 66px;
}
</style>
