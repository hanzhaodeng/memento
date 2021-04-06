<template>
  <v-container>
    <v-row>
      <v-col>
        <v-dialog v-model="dialog" width="290">
          <template v-slot:activator="{ on, attrs }">
            <h1
              class="text-center font-weight-light project-title"
              v-bind="attrs"
              v-on="on"
            >
              Memento Mori
            </h1>
          </template>
          <v-card>
            <v-date-picker
              :value="brithday"
              @input="setBrithday"
            ></v-date-picker>
          </v-card>
        </v-dialog>
      </v-col>
    </v-row>
    <br />
    <mori :value="weeks" />
  </v-container>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Mori from "@/components/Mori.vue";
import { DateTime } from "luxon";

@Component({
  components: {
    Mori
  }
})
export default class Home extends Vue {
  private brithday: string =
    localStorage.getItem("bday") ?? new Date().toISOString().substr(0, 10);

  setBrithday(value: string) {
    localStorage.setItem("bday", value);
    this.brithday = value;
  }

  dialog = false;

  get weeks(): number {
    const birthday = DateTime.fromISO(this.brithday);
    return -Math.floor(birthday.diffNow("weeks").toObject().weeks ?? 0);
  }
}
</script>

<style scoped>
.project-title {
  font-family: "Monoton", cursive;
  font-size: 92px;
  background: -webkit-linear-gradient(#00d672, rgb(148, 3, 129));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
</style>
