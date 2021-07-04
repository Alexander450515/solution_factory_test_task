<template>
  <div>
    <v-row v-for="(range, i) in this.condition.cardType" :key="i">
      <v-col>
        <p>{{ `Тип ${++i}` }}</p>
      </v-col>
      <v-col cols="6">
        <select v-model="cardType" class="condition__input">
          <option>Gold</option>
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
    cardType: {
      get() {
        if (this.condition !== null) return this.condition.cardType[0]
      },
      set(value) {
        if (this.condition !== null) this.condition.cardType[0] = value
      },
    },
  },
}
</script>

<style>
.condition-2 {
  background-color: rgb(224, 224, 250);
}
.condition-2__title {
  color: rgb(72, 47, 214);
  font: 1em 'Fira Sans', sans-serif;
  font-weight: 600;
  align-self: center;
}
</style>
