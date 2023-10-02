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
          :cozy_places="chat.cozy_places"
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
import ChatBoxBot from "./ChatBoxBot.vue";
import ChatBoxUser from "./ChatBoxUser.vue";
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
        {
          img_name: "black_cat.jpeg",
          isBot: true,
          text: "Hello",
          cozy_places: [
            {
              name: "신림역",
              latitude: 37.48424187396406,
              longitude: 126.92968999635784,
            },
          ],
        },
        {
          img_name: "white_cat.png",
          isBot: false,
          text: "How are you?",
        },
        {
          img_name: "black_cat.jpeg",
          isBot: true,
          text: "Hello",
          cozy_places: [],
        },
        {
          img_name: "white_cat.png",
          isBot: false,
          text: "How are you?",
        },
        {
          img_name: "black_cat.jpeg",
          isBot: true,
          text: "Hello",
          cozy_places: [
            {
              name: "신림역",
              latitude: 37.48424187396406,
              longitude: 126.92968999635784,
            },
            {
              name: "신림역",
              latitude: 37.48424187396406,
              longitude: 126.92968999635784,
            },
            {
              name: "신림역",
              latitude: 37.48424187396406,
              longitude: 126.92968999635784,
            },
          ],
        },
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
