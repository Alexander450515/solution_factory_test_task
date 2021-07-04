<template>
  <v-card class="respondents">
    <v-card-title class="respondents_title">Добавить опрос</v-card-title>

    <condition-template
      v-for="(condition, index) in conditions"
      :key="index"
      :conditions="conditions"
      :condition="condition"
      :index="index"
    />
    <v-card-text class="condition-add-btn" @click="addCondition">
      <v-icon x-large>mdi-plus</v-icon>
      <p>Нажмите, чтобы добавить новое условие выборки.</p>
      <p>Все условия связываются между собой логическими "И".</p>
    </v-card-text>

    <v-card-actions>
      <v-btn small color="rgb(74, 219, 74)" outlined text
        >Протестировать опрос</v-btn
      >
      <v-spacer></v-spacer>
      <v-btn small color="rgb(74, 219, 74)" dark @click="continueInterview"
        >Далее</v-btn
      >
    </v-card-actions>
  </v-card>
</template>

<script>
import conditionTemplate from '@/components/interview/respondents/condition-template.vue'

export default {
  components: {
    'condition-template': conditionTemplate,
  },
  data() {
    return {
      conditions: [],
    }
  },
  methods: {
    addCondition() {
      console.log('addCondition')
      this.conditions.push({
        conditionName: 'Возраст респондента',
        id: this.conditions.length + 1,
        ranges: [],
        cardType: [],
        status: [],
      })
    },
    async continueInterview() {
      console.log('sendFrom')
      try {
        await this.$axios.$post('/someapi', this.conditions)
      } catch (error) {
        console.log(error.message)
      }
    },
  },
}
</script>

<style>
.respondents {
  border: 1px solid rgb(146, 233, 146);
  /* height: 90vh; */
  box-shadow: 5px 5px 15px 2px rgb(206, 206, 206);
}
.respondents_title {
  padding: 20px 25px 30px 25px;
  color: grey;
  font: 0.8em 'Fira Sans', sans-serif;
}

.condition__input {
  border: 1px solid gray;
  border-radius: 7px;
  padding: 5px;
  align-self: center;
  background-color: white;
  width: 100%;
}
.condition_btn {
  background-color: white;
}
.condition-add-btn {
  border: 1px solid gray;
  text-align: center;
  cursor: pointer;
}
</style>
