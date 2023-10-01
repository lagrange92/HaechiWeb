<template>
  <div class="chat-input">
    <input
      type="text"
      v-model="newMessage"
      class="input-border"
      style="height: 35px; margin: 10px"
      @keyup.enter="sendMessage"
    />
    <v-btn @click="sendMessage" color="green-darken-1">Send</v-btn>
  </div>
</template>

<script>
export default {
  name: "ChatInput",
  data() {
    return {
      newMessage: "",
    };
  },
  methods: {
    sendMessage() {
      this.$emit("new-message", this.newMessage);
      this.newMessage = "";
    },
  },
};
</script>

<style>
.chat-input {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: "purple";
}

.chat-input input {
  width: 80%;
}

.chat-input v-btn {
  border: none;
  cursor: pointer;
}

.input-border {
  border: 1px solid #ccc; /* 테두리 선 스타일 지정 */
  border-radius: 5px; /* 테두리 선 둥글게 처리 */
  box-shadow: 0 0 5px #ccc; /* 시어 효과 지정 */
  height: 35px;
  margin: 10px;
  padding: 5px;
}
</style>
