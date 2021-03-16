<template>
  <div class="home">
    <Mori />
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
