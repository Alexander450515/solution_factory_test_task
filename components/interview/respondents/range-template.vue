<template>
  <div>
    <v-row v-for="(range, i) in this.condition.ranges" :key="i">
      <v-col>
        <p>{{ `Диапазон ${++i}` }}</p>
      </v-col>
      <v-col cols="8">
        от&nbsp;
        <input type="text" class="range_input" v-model="rangeStart" />
        до&nbsp;
        <input v-model="rangeEnd" type="text" class="range_input" />
      </v-col>
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
    rangeStart: {
      get() {
        if (this.condition !== null) return this.condition.ranges[0].start
      },
      set(value) {
        if (this.condition !== null) this.condition.ranges[0].start = value
      },
    },
    rangeEnd: {
      get() {
        if (this.condition !== null) return this.condition.ranges[0].end
      },
      set(value) {
        if (this.condition !== null) this.condition.ranges[0].end = value
      },
    },
  },
}
</script>
