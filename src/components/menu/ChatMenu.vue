<template>
  <div class="chat">
    <div class="chat-messages">
      <div v-for="message in messages" :key="message.id">
        {{ message.text }}
      </div>
    </div>
    <div class="chat-input">
      <input type="text" v-model="newMessage" />
      <button @click="sendMessage">Send</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "ChatMenu",
  data() {
    return {
      messages: [
        { id: 1, text: "Hello" },
        { id: 2, text: "How are you?" },
      ],
      newMessage: "",
    };
  },
  methods: {
    sendMessage() {
      if (this.newMessage) {
        this.messages.push({
          id: this.messages.length + 1,
          text: this.newMessage,
        });
        this.newMessage = "";
      }
    },
  },
};
</script>

<style>
.chat {
  padding: 10px;
  border-bottom: 1px solid #ccc;
}

.chat-messages {
  height: 300px;
  overflow-y: scroll;
}

.chat-input {
  margin-top: 10px;
}

.chat-input input {
  width: 80%;
  margin-right: 10px;
}

.chat-input button {
  background-color: #007bff;
  color: #fff;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
}
</style>
