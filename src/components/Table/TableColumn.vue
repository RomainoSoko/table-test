<template>
  <slot :item="item" v-if="item" />
</template>

<script>
export default {
  name: 'Table-Column',
  props: {
    prop: {
      type: String,
      required: true,
    },
    label: {
      type: String,
      required: true,
    },
  },
  setup() {
    const item = null;

    return { item };
  },
};
</script>

<style scoped>

</style>
