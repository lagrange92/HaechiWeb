<template>
  <div
    class="chat-messages-container"
    :style="{ backgroundColor: 'rgba(51, 105, 30, 0.6)' }"
  >
    <div class="chat-inner-cont">
      <div
        class="chat-messages"
        ref="chatMessages"
        :style="{ backgroundColor: '#DCEDC8', opacity: 0.8 }"
      >
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
      <ChatInput class="chat-input" @new-message="sendMessage" />
    </div>
  </div>
</template>

<script>
import ChatBoxBot from "./ChatBoxBot.vue";
import ChatBoxUser from "./ChatBoxUser.vue";
import ChatInput from "./ChatInput.vue";

import axios from "axios";

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
      if (newMessage == "") {
        return;
      }

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

      axios
        .post("http://localhost:1323/chat", {
          prompt: newMessage,
        })
        .then((response) => {
          this.chats.push({
            isBot: true,
            img_name: "black_cat.jpeg",
            text: response.data,
          });

          this.$nextTick(() => {
            // scrollToBottom
            this.$refs.chatMessages.scrollTop =
              this.$refs.chatMessages.scrollHeight;
          });
        });
    },
  },
};
</script>

<style>
.chat-messages-container {
  height: 100%;
  border-radius: 10px;
}

.chat-inner-cont {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100%;
  padding: 20px;
}

.chat-messages {
  display: flex;
  flex-direction: column;
  height: 90%;
  overflow-y: scroll;
  background-color: yellowgreen;
  padding: 10px;
  border-radius: 10px;
}

.chat-input {
  height: 7%;
}
</style>
