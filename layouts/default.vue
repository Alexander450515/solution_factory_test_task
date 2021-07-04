<template>
  <div class="main">
    <div id="side-nav" class="side-nav">
      <div
        v-for="item in sideBarItems"
        :key="item.icon"
        :class="['side-nav__btn', { active: currentItem === item.icon }]"
        @click="currentItem = item.icon"
      >
        <nuxt-link :to="item.link" class="link">
          <v-icon x-large>{{ item.icon }}</v-icon>
          <p>{{ item.description }}</p>
        </nuxt-link>
      </div>
    </div>
    <div class="container">
      <div class="app-bar">
        <input type="text" class="app-bar__input" />
        <div class="app-bar__user">
          <v-avatar size="36">
            <img src="https://cdn.vuetifyjs.com/images/john.jpg" alt="John" />
          </v-avatar>
          <div class="app-bar__user__name">
            <h3>Alexander C.</h3>
            <p>Администратор</p>
          </div>
        </div>
      </div>
      <Nuxt />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentItem: 'mdi-note-text-outline',
      sideBarItems: [
        {
          description: '',
          icon: 'mdi-checkbox-blank-circle',
          link: '',
        },
        {
          description: 'Опросы',
          icon: 'mdi-note-text-outline',
          link: '/',
        },
        {
          description: 'Пользователи',
          icon: 'mdi-account-multiple-outline',
          link: '/users',
        },
        {
          description: 'Черные списки',
          icon: 'mdi-flag-variant-outline',
          link: '/blacklist',
        },
        {
          description: 'Колл центр',
          icon: 'mdi-phone',
          link: '/callcenter',
        },
      ],
    }
  },
}
</script>

<style>
.main {
  display: flex;
}

.app-bar {
  display: flex;
  justify-content: space-between;
  flex: 1;
}

.app-bar__input {
  border: 1px solid black;
  border-radius: 7px;
  width: 60%;
  height: 3vh;
  align-self: center;
  padding: 5px;
}

.app-bar__user {
  display: flex;
  flex-direction: row;
}

.app-bar__user__name {
  align-self: center;
  font: 0.7em 'Fira Sans', sans-serif;
  margin-left: 3px;
}

.side-nav {
  display: flex;
  flex-direction: column;
  height: 100vh;
  width: 120px;
  border-right: 2px solid rgb(226, 225, 225);
}

.side-nav__btn {
  display: flex;
  flex-direction: column;
  margin: 5px;
  height: 70px;
  text-align: center;
  border-radius: 10px;
}
.side-nav__btn:hover {
  background: rgb(232, 236, 232);
}
.side-nav__btn.active {
  border: 2px solid rgb(74, 219, 74);
}
.link {
  text-decoration: none;
  font: 0.7em 'Fira Sans', sans-serif;
  margin: 5px;
  color: black;
}
</style>
