<template>
  <v-card-text class="condition-1">
    <v-row>
      <v-col>
        <p class="condition-1__title">
          {{ `Условие ${this.condition.id}` }}
        </p>
      </v-col>
      <v-col cols="8">
        <select v-model="option" class="condition__input">
          <option>Возраст респондента</option>
          <option>Тип карты лояльности</option>
          <option>Статус карты лояльности</option>
        </select>
      </v-col>
    </v-row>

    <range-template
      v-if="option === 'Возраст респондента'"
      :condition="condition"
      :index="index"
      :conditions="conditions"
    />
    <type-template
      v-if="option === 'Тип карты лояльности'"
      :condition="condition"
      :index="index"
      :conditions="conditions"
    />
    <status-template
      v-if="option === 'Статус карты лояльности'"
      :condition="condition"
      :index="index"
      :conditions="conditions"
    />

    <v-row>
      <v-col></v-col>
      <v-col cols="5">
        <v-btn
          v-if="this.currentConditionBtn"
          small
          color="rgb(74, 219, 74)"
          outlined
          class="condition_btn"
          @click="addCurrentCondition"
        >
          {{ this.currentConditionBtn }}</v-btn
        >
      </v-col>
      <v-col cols="3">
        <v-btn
          small
          color="rgb(219, 74, 74)"
          outlined
          class="condition_btn"
          @click="deleteCondition(index)"
          >Удалить условие</v-btn
        >
      </v-col>
    </v-row>
  </v-card-text>
</template>

<script>
import rangeTemplate from './range-template.vue'
import typeTemplate from './type-template.vue'
import statusTemplate from './status-template.vue'

export default {
  components: {
    'range-template': rangeTemplate,
    'type-template': typeTemplate,
    'status-template': statusTemplate,
  },
  props: {
    conditions: Array,
    condition: Object,
    index: Number,
  },
  computed: {
    currentConditionBtn() {
      switch (this.condition.conditionName) {
        case 'Возраст респондента':
          return 'Добавить диапазон'

        case 'Тип карты лояльности':
          return 'Добавить тип'

        case 'Статус карты лояльности':
          return 'Добавить статус'
      }
    },
    option: {
      get() {
        return this.condition.conditionName
      },
      set(value) {
        this.condition.conditionName = value
      },
    },
  },
  methods: {
    addCurrentCondition() {
      if (this.currentConditionBtn === 'Добавить диапазон')
        this.condition?.ranges.push({
          start: 0,
          end: 0,
        })
      if (this.currentConditionBtn === 'Добавить тип')
        this.condition?.cardType.push('')
      if (this.currentConditionBtn === 'Добавить статус')
        this.condition?.status.push('')
    },
    deleteCondition(index) {
      console.log('deleteCondition', index)
      this.conditions.splice(index, 1)
    },
  },
}
</script>

<style>
.condition-1 {
  background-color: rgb(241, 234, 224);
}
.condition-1__title {
  color: rgb(214, 136, 47);
  font: 1em 'Fira Sans', sans-serif;
  font-weight: 600;
  align-self: center;
}
.range_input {
  border: 1px solid black;
  border-radius: 7px;
  padding: 5px;
  width: 10%;
  height: 2.5vh;
  align-self: center;
  background-color: white;
}
</style>
