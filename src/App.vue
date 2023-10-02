<template>
  <div id="app">
    <v-layout class="menu-layout">
      <v-navigation-drawer
        :rail="rail"
        :width="500"
        permanent
        @click="rail = false"
        :style="{ backgroundColor: '#F1F8E9' }"
      >
        <v-list-item title="Hingy" nav class="menu-top">
          <template v-slot:prepend>
            <v-avatar :image="require('@/assets/white_cat.png')"> </v-avatar>
          </template>
          <template v-slot:append>
            <v-btn
              variant="text"
              icon="mdi-chevron-left"
              @click.stop="rail = !rail"
            ></v-btn>
          </template>
        </v-list-item>
        <div
          style="
             {
              margin: 10px;
              padding: 10px;
              padding-right: 30px;
            }
          "
          :style="{ height: chatboxHeight }"
        >
          <transition name="fade">
            <ChatMenu v-show="!rail" class="chat-menu" />
          </transition>
        </div>
      </v-navigation-drawer>
      <v-main> </v-main>
    </v-layout>
    <NaverMap class="map" :route="route" />
  </div>
</template>

<script>
import NaverMap from "./components/NaverMap.vue";
import ChatMenu from "./components/menu/Chat/ChatMenu.vue";

export default {
  name: "App",
  components: {
    NaverMap,
    ChatMenu,
  },
  mounted() {
    window.addEventListener("resize", this.updateChatboxHeight);
    this.updateChatboxHeight();

    // Trick for loading naver map properly
    this.$nextTick(() => {
      this.rail = false;
    });
  },
  beforeMount() {
    window.removeEventListener("resize", this.updateChatboxHeight);
  },
  data() {
    return {
      menuOpen: true,
      rail: true,
      panelOpen: [0], // expand panels which index is located in panelOpen array
      route: [],
      chatboxHeight: "",
      mainLayoutWidth: "",
      mapKey: 0,
    };
  },
  methods: {
    updateMapWidth() {},
    updateChatboxHeight() {
      const menuTopHeight = document.querySelector(".menu-top").offsetHeight;
      const chatboxTopSpace = 40;
      this.chatboxHeight = `${
        window.innerHeight - chatboxTopSpace - menuTopHeight
      }px`;
    },
    getRoute(resultPaths) {
      console.log(resultPaths);

      this.route = resultPaths;
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  width: 100%;
  height: 100vh;
  display: flex;
  background-color: "purple-darken-2";
}

.menu {
  width: 70px;
  height: 100%;
  border-right: 1px solid grey;
  transition: all 0.4s ease-in-out;
  margin-right: 20px;
}

.menu-open {
  width: 40%;
}

.chat-menu {
  height: 100%;
}

.map {
  width: 100%;
  height: 100%;
  background-color: white;
}

.user {
  display: flex;
  height: 50px;
  align-items: center;
  padding: 0px;
  margin: 0px;
}

.user-name {
  display: flex;
  margin: 0px;
  margin-left: 25px;
  padding: 0px;
  width: 80%;
  height: 50px;
  align-items: center;
}

.collapse-btn {
  font-size: 24px;
}

.fade-enter-active {
  transition: opacity 0.3s ease-out 0.3s;
}

.fade-enter-from, .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}

.menu .v-expansion-panel-text__wrapper {
  padding: 5px 10px 5px 10px;
}
</style>
