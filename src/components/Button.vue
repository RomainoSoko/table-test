<template>
  <button class="bg-blue-600 p-4 flex items-center justify-center">
    <slot />
  </button>
</template>
<script>
export default {
  name: 'button-el',
  setup() {
    return {};
  },
};
</script>
