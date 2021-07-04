<template>
  <div>
    <v-row v-for="(range, i) in this.condition.status" :key="i">
      <v-col>
        <p>{{ `Статус ${++i}` }}</p>
      </v-col>
      <v-col cols="6">
        <select v-model="status" class="condition__input">
          <option>Активна</option>
        </select>
      </v-col>
      <v-col cols="2"></v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  props: {
    conditions: Array,
    condition: Object,
    index: Number,
  },
  computed: {
    status: {
      get() {
        if (this.condition !== null) return this.condition.status[0]
      },
      set(value) {
        if (this.condition !== null) this.condition.status[0] = value
      },
    },
  },
}
</script>

<style>
.condition-3 {
  background-color: rgb(224, 250, 226);
}
.condition-3__title {
  color: rgb(24, 175, 57);
  font: 1em 'Fira Sans', sans-serif;
  font-weight: 600;
  align-self: center;
}
</style>
