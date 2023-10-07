<template>
  <div class="chat-input">
    <textarea
      v-model="newMessage"
      class="input-border"
      :style="{ color: 'white', height: '100%' }"
      @keydown.enter="updateMessage"
    />
    <div class="btn-cont">
      <v-btn
        @click="sendMessage"
        color="green-darken-1"
        :style="{ height: '100%' }"
        >Send</v-btn
      >
    </div>
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
  width: 100%;
  resize: none;
  padding: 10px;
}

.chat-input .btn-cont {
  height: 100%;
  padding-left: 10px;
}

.chat-input .btn-cont v-btn {
  border: none;
  cursor: pointer;
  width: 100%;
}

.input-border {
  border: 1px solid #ccc; /* 테두리 선 스타일 지정 */
  border-radius: 5px; /* 테두리 선 둥글게 처리 */
  box-shadow: 0 0 5px #ccc; /* 시어 효과 지정 */
  height: 100%;
}
</style>
