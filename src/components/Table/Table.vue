<template>
  <div class="hidden">
    <slot></slot>
  </div>

  <div class="overflow-x-auto">
    <table class="w-full">
      <thead>
      <th
        v-for="col in columns"
        :key="col.prop"
      >{{ col.label }}
      </th>
      </thead>
      <TableBody
        :data="data"
        :columns="columns"
      />
    </table>
  </div>
</template>

<script>
import TableBody from '@/components/Table/TableBody';
import { computed } from 'vue';

export default {
  name: 'Table-el',
  components: {
    TableBody,
  },
  props: {
    data: {
      type: Array,
      default: () => [],
    },
  },
  setup(props, ctx) {
    const columns = computed(() => ctx.slots.default().map((slot) => {
      return {
        content: slot.children?.default ? slot.children.default : null,
        ...slot.props,
      };
    }));
    return {
      columns,
    };
  },
};
</script>
