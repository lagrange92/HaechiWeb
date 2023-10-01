<template>
  <div class="chat-box-bot">
    <ChatImg :img_name="img" />
    <span style="margin-left: 10px"></span>
    <ChatContent :content="content" />
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
  },
};
</script>

<style>
.chat-box-bot {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  align-items: center;
}
</style>
