<template>
  <input type="text" v-model="search" class="bg-gray-200">
  <button class="bg-red-100 p-2" @click="mutate">
    Mutate
  </button>
  <Table :data="getItems">
    <TableColumn
      prop="date"
      label="Date"
    />
    <TableColumn
      prop="name"
      label="Name"
      v-slot:default="slotProps"
    >
      <Button>{{ slotProps?.item.name }}</Button>
    </TableColumn>
    <TableColumn
      prop="address"
      label="Address"
    >
      hihi
    </TableColumn>
  </Table>
</template>

<script>
import Table from '@/components/Table/Table.vue';
import TableColumn from '@/components/Table/TableColumn.vue';
import Button from '@/components/Button.vue';
import { computed, ref } from 'vue';

export default {
  name: 'App',
  components: {
    Button,
    Table,
    TableColumn,
  },
  setup() {
    const search = ref('');

    const mutate = () => {
      items.value[0].name = (Math.random() + 1).toString(36).substring(7);
    };

    const items = ref([
      {
        date: '2016-05-03',
        name: 'Tom',
        address: 'No. 189, Grove St, Los Angeles',
      },
      {
        date: '2016-05-02',
        name: 'Bilooouuuu',
        address: 'No. 189, Grove St, Los Angeles',
      },
    ]);

    const getItems = computed(() => items.value.filter(o => o.name.includes(search.value)));

    return {
      search,
      items,
      getItems,
      mutate,
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
