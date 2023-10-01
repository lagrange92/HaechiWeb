<template>
  <div class="chat-box-user">
    <ChatContent :content="content" />
    <span style="margin-left: 10px"></span>
    <ChatImg :img_name="img" />
  </div>
</template>

<script>
import ChatImg from "./ChatImg.vue";
import ChatContent from "./ChatContent.vue";

export default {
  name: "UserMsgBox",
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
.chat-box-user {
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  align-items: center;
}
</style>
