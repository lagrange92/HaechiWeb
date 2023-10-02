<template>
  <div id="app">
    <div class="menu" :class="{ 'menu-open': menuOpen }">
      <div class="user">
        <transition name="fade">
          <p class="user-name" v-if="menuOpen">John Doe</p>
        </transition>
        <v-btn class="collapse-btn" elevation="0" @click="menuOpen = !menuOpen">
          <span v-if="menuOpen">&laquo;</span>
          <span v-else>&raquo;</span>
        </v-btn>
      </div>
      <v-expansion-panels v-model="panelOpen">
        <transition name="fade">
          <v-expansion-panel
            title="Chatting"
            v-show="menuOpen"
            v-model="panelOpen"
          >
            <v-expansion-panel-text style="margin-top: 10px">
              <ChatMenu />
            </v-expansion-panel-text>
          </v-expansion-panel>
        </transition>
        <transition name="fade">
          <v-expansion-panel title="Routing" v-show="menuOpen">
            <v-expansion-panel-text>
              <RouteMenu @resultPaths="getRoute" />
            </v-expansion-panel-text>
          </v-expansion-panel>
        </transition>
      </v-expansion-panels>
    </div>
    <NaverMap class="map" :route="route" />
  </div>
</template>

<script>
import NaverMap from "./components/NaverMap.vue";
import ChatMenu from "./components/menu/Chat/ChatMenu.vue";
import RouteMenu from "./components/menu/RouteMenu.vue";

export default {
  name: "App",
  components: {
    NaverMap,
    ChatMenu,
    RouteMenu,
  },
  data() {
    return {
      menuOpen: true,
      panelOpen: [1], // expand panels which index is located in panelOpen array
      route: [],
    };
  },
  methods: {
    getRoute(resultPaths) {
      console.log("getRoute");
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
}

.menu {
  width: 70px;
  height: 100%;
  border-right: 1px solid grey;
  transition: all 0.4s ease-in-out;
}

.menu-open {
  width: 25%;
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
