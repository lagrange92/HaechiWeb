<template>
  <div :style="{ backgroundColor: 'purple-darken-2' }">
    <v-card max-width="210px" variant="elevated" color="green-lighten-1">
      <v-card-text>
        <div v-for="(t, k) in content.split('\n')" :key="k">
          {{ t }}
        </div>
      </v-card-text>
    </v-card>
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
    cozy_places: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<style></style>
