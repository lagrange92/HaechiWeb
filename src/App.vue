<template>
  <div class="app">
    <v-layout class="menu-layout" justify-end>
      <v-navigation-drawer
        rail
        class="menu-drawer"
        expand-on-hover
        @mouseover="menuExpand = true"
        @mouseleave="menuExpand = false"
        @click="rail = false"
        :style="{ backgroundColor: 'rgba(51, 105, 30, 0.6)', color: 'white' }"
      >
        <div>
          <v-list density="compact" nav>
            <v-list-item
              prepend-icon="mdi-home"
              title="Home"
              @click="clickHome()"
            ></v-list-item>
            <v-list-item
              prepend-icon="mdi-chat"
              title="Chat"
              @click="clickChat()"
            ></v-list-item>
            <v-list-item
              prepend-icon="mdi-map"
              title="Map"
              @click="clickMap()"
            ></v-list-item>
          </v-list>
        </div>
        <div>
          <v-divider></v-divider>

          <v-list density="compact" nav>
            <v-list-item title="Hingy" nav class="menu-top">
              <template v-slot:prepend>
                <v-avatar
                  :image="require('@/assets/white_cat.png')"
                  @click.stop="rail = !rail"
                >
                </v-avatar>
              </template>
            </v-list-item>
            <v-list-item
              prepend-icon="mdi-cog"
              title="Setting"
              value="Setting"
            ></v-list-item>
          </v-list>
        </div>
      </v-navigation-drawer>
      <v-main> </v-main>
    </v-layout>
    <div class="main-cont" :class="{ 'shrink-main-cont': menuExpand }">
      <transition name="fade">
        <div class="chat-cont" :class="{ 'shrink-cont': showMode == 'map' }">
          <ChatMenu class="chat-menu" />
        </div>
      </transition>
      <transition name="fade">
        <div class="map-cont" :class="{ 'shrink-cont': showMode == 'chat' }">
          <NaverMap :route="route" />
        </div>
      </transition>
    </div>
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
      this.showMode = "home";
      this.rail = false;
    });
  },
  beforeMount() {
    window.removeEventListener("resize", this.updateChatboxHeight);
  },
  data() {
    return {
      showMode: "map", // showMode - home, chat, map
      menuExpand: false,
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
    clickHome() {
      this.showMode = "home";
    },
    clickChat() {
      if (this.showMode === "chat") {
        this.showMode = "home";
      } else {
        this.showMode = "chat";
      }
    },
    clickMap() {
      if (this.showMode === "map") {
        this.showMode = "home";
      } else {
        this.showMode = "map";
      }
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

.app {
  width: 100%;
  height: 100vh;
  display: flex;
  background-image: url("@/assets/background.png");
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
}

.menu-drawer:hover {
  width: 10% !important;
  transition: width 0.55s;
}

.main-cont {
  display: flex;
  flex-direction: row;
  width: 100%;
  height: 100%;
  justify-content: space-around;
  align-items: center;
  transition: width 0.5s;
}

.shrink-main-cont {
  width: 90%;
  transition: width 0.5s;
}

.chat-cont {
  padding: 10px;
  padding-left: 20px;
  width: 100%;
  height: 90%;
  transition: width 0.5s;
}

.map-cont {
  padding: 10px;
  padding-right: 20px;
  width: 100%;
  height: 90%;
  transition: width 0.5s;
}

.shrink-cont {
  width: 0%;
  transition: width 0.5s;
}

.menu-top {
  cursor: pointer;
}

.menu-open {
  width: 40%;
}

.chat-menu {
  height: 100%;
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

.fade-enter-active,
.fade-leave-active {
  transition: all 0.5s ease;
}

.fade-enter-from, .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}

.menu-layout .v-navigation-drawer__content {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  opacity: 0.5;
}
</style>
