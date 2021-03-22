<template>
  <div>
    <v-row>
      <v-col>
        <v-dialog v-model="dialog" width="290">
          <template v-slot:activator="{ on, attrs }">
            <h1
              class="text-h3 text-center font-weight-bold"
              v-bind="attrs"
              v-on="on"
            >
              Memento Mori
            </h1>
          </template>
          <v-card>
            <v-date-picker
              :value="brithdayData"
              @input="setBrithday"
            ></v-date-picker>
          </v-card>
        </v-dialog>
      </v-col>
    </v-row>
    <br />
    <Mori :value="weeks" />
  </div>
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
  private brithdayData =
    localStorage.getItem("bday") ?? new Date().toISOString().substr(0, 10);

  setBrithday(value: string) {
    localStorage.setItem("bday", value);
    this.brithdayData = value;
  }

  dialog = false;

  get weeks(): number {
    const birthday = DateTime.fromISO(this.brithdayData);
    return -Math.floor(birthday.diffNow("weeks").toObject().weeks ?? 0);
  }
}
</script>
