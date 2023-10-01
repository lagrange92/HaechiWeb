<template>
  <div>
    <div class="chat-messages" ref="chatMessages">
      <div
        v-for="chat in chats"
        :key="chat.img_name"
        style="padding-bottom: 20px"
      >
        <ChatBoxBot
          v-if="chat.isBot"
          :img="chat.img_name"
          :content="chat.text"
        />
        <ChatBoxUser v-else :img="chat.img_name" :content="chat.text" />
      </div>
    </div>
    <span
      style="
         {
          margin-bottom: 20px;
        }
      "
    ></span>
    <ChatInput
      @new-message="sendMessage"
      style="height: 50px; margin-top: 5px"
    />
  </div>
</template>

<script>
import ChatBoxBot from "./ChatBoxUser.vue";
import ChatBoxUser from "./ChatBoxBot.vue";
import ChatInput from "./ChatInput.vue";

export default {
  name: "ChatMenu",
  components: {
    ChatBoxBot,
    ChatBoxUser,
    ChatInput,
  },
  data() {
    return {
      chats: [
        { img_name: "black_cat.jpeg", isBot: true, text: "Hello" },
        {
          img_name: "white_cat.png",
          isBot: false,
          text: "How are you?",
        },
        { img_name: "black_cat.jpeg", isBot: true, text: "Hello" },
        {
          img_name: "white_cat.png",
          isBot: false,
          text: "How are you?",
        },
        { img_name: "black_cat.jpeg", isBot: true, text: "Hello" },
      ],
    };
  },
  methods: {
    sendMessage(newMessage) {
      if (newMessage) {
        this.chats.push({
          isBot: false,
          img_name: "white_cat.png",
          text: newMessage,
        });

        this.$nextTick(() => {
          // scrollToBottom
          this.$refs.chatMessages.scrollTop =
            this.$refs.chatMessages.scrollHeight;
        });
      }
    },
  },
};
</script>

<style>
.chat-messages {
  display: flex;
  flex-direction: column;
  height: 400px;
  overflow-y: scroll;
}
</style>
