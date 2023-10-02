<template>
  <div class="chat-box-bot">
    <div class="chat-box-msg">
      <ChatImg :img_name="img" />
      <span style="margin-left: 10px"></span>
      <ChatContent :content="content" :cozy_places="cozy_places" />
    </div>
    <div class="cozy-btn-container">
      <v-btn
        class="cozy-btn"
        color="blue"
        @click="showRoutePage"
        v-for="(cozy, key) in cozy_places"
        :key="key"
        :value="cozy"
        >{{ cozy.name }}
      </v-btn>
      <space-holder></space-holder>
    </div>
  </div>
</template>

<script>
import ChatImg from "./ChatImg.vue";
import ChatContent from "./ChatContent.vue";

export default {
  name: "BotMsgBox",
  components: {
    ChatImg,
    ChatContent,
  },
  props: {
    img: {
      type: String,
      required: true,
    },
    content: {
      type: String,
      required: true,
    },
    cozy_places: {
      type: Array,
      default: () => [],
    },
  },
  methods: {
    showRoutePage(event) {
      let cozy = JSON.parse(event.target.value);

      let url =
        "https://map.kakao.com/link/to/" +
        cozy.name +
        ", " +
        cozy.latitude +
        ", " +
        cozy.longitude;

      window.open(url, "_blank");
    },
  },
};
</script>

<style>
.chat-box-bot {
  display: flex;
  flex-direction: column;
}

.chat-box-msg {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  align-items: center;
}

.cozy-btn-container {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  margin-top: 10px;
  margin-bottom: 10px;
}

.cozy-btn {
  margin-right: 10px;
}
</style>
