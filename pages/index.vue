<template>
  <div class="interview">
    <div class="dynamic-component">
      <button
        v-for="tab in tabs"
        v-bind:key="tab.component"
        v-bind:class="['tab-button', { active: currentTab === tab.component }]"
        v-on:click="currentTab = tab.component"
      >
        {{ tab.description }}
      </button>
      <div class="container">
        <keep-alive>
          <component :is="currentTab"> </component>
        </keep-alive>
      </div>
    </div>
  </div>
</template>

<script>
import params from '@/components/interview/params'
import logic from '@/components/interview/logic'
import conditions from '@/components/interview/conditions'
import questions from '@/components/interview/questions'
import respondents from '@/components/interview/respondents'

export default {
  components: {
    params,
    logic,
    conditions,
    questions,
    respondents,
  },
  data() {
    return {
      currentTab: 'params',
      tabs: [
        { description: 'Параметры', component: 'params' },
        { description: 'Вопросы', component: 'questions' },
        { description: 'Логика', component: 'logic' },
        { description: 'Условия', component: 'conditions' },
        { description: 'Респонденты', component: 'respondents' },
      ],
    }
  },
  computed: {
    currentTabComponent() {
      return this.currentTab
    },
  },
}
</script>

<style>
.dynamic-component {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr;
  grid-template-rows: 1fr;
  gap: 0px 0px;
  grid-template-areas:
    '. . . . .'
    'container container container container container';
  margin-top: 6px;
}
.tab-button {
  padding: 6px 10px;
  cursor: pointer;
}
.tab-button:hover {
  background: rgb(195, 255, 195);
  border-bottom: 4px solid rgb(74, 219, 74);
}
.tab-button.active {
  border-bottom: 4px solid rgb(74, 219, 74);
}
.container {
  grid-area: container;
  padding: 0;
}
</style>
