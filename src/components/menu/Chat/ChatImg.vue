<template>
  <v-avatar :image="require('@/assets/' + img_name)" size="50"></v-avatar>
</template>

<script>
export default {
  props: {
    img_name: {
      type: String,
      required: true,
    },
  },
};
</script>

<style></style>
