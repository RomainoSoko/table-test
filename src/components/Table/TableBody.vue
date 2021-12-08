<script>
import { defineComponent, h } from 'vue';

export default defineComponent({
  name: 'Table-Body',
  props: {
    data: {
      type: Array,
      default: () => [],
    },
    columns: {
      type: Array,
      default: () => [],
    },
  },
  setup(props) {
    const defaultProps = {
      class: 'cell',
    };

    const colRender = (col, row, $index) => {
      const colContent = col.content ? col.content({ item: row }) : props.data[$index][col.prop];

      return h('div', {
        ...defaultProps,
      }, [colContent]);
    };

    const rowRender = (row, $index) => {
      return h('tr', {}, props.columns.map((column) => {
        return h('td', {
          style: {
            minWidth: '200px',
          },
        }, colRender(column, row, $index));
      }));
    };

    const wrappedRowRender = (row, $index) => {
      return rowRender(row, $index);
    };
    return {
      rowRender,
      wrappedRowRender,
    };
  },
  render() {
    return h('tbody', {}, [
      this.data.reduce((rows, row) => {
        return rows.concat(this.wrappedRowRender(row, rows.length));
      }, []),
    ]);
  },
});
</script>
