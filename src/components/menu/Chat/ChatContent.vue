<template>
  <div>
    <v-card
      max-width="210px"
      :text="content"
      variant="elevated"
      color="green-lighten-1"
    ></v-card>
  </div>
</template>

<script>
export default {
  name: "ChatContent",
  props: {
    content: {
      type: String,
      required: true,
    },
  },
};
</script>

<style></style>
