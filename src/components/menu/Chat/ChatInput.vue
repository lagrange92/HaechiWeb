<template>
  <div class="chat-input" :style="{ backgrounColor: 'red' }">
    <textarea
      v-model="newMessage"
      class="input-border"
      @keydown.enter="updateMessage"
    />
    <v-btn @click="sendMessage" color="green-darken-1" height="100%"
      >Send</v-btn
    >
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
    updateMessage(event) {
      if (event.shiftKey) {
        return;
      }
      if (event.keyCode === 13) {
        this.sendMessage();
        event.preventDefault();
      }
    },
    sendMessage() {
      if (this.newMessage === "") return;

      console.log("newMessage: ", this.newMessage);

      this.$emit("new-message", this.newMessage);
      this.newMessage = "";
    },
  },
};
</script>

<style>
.chat-input {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}

.chat-input textarea {
  width: 80%;
  resize: none;
  padding: 10px;
}

.chat-input v-btn {
  border: none;
  cursor: pointer;
}

.input-border {
  border: 1px solid #ccc; /* 테두리 선 스타일 지정 */
  border-radius: 5px; /* 테두리 선 둥글게 처리 */
  box-shadow: 0 0 5px #ccc; /* 시어 효과 지정 */
  height: 100%;
  /* margin: 0px 10px 0px 0px; */
  /* margin-right: 10px; */
  /* padding: 5px; */
}
</style>
