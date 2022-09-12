<template>
  <div class="table">
    <div class="header" v-for="header in headers" :key="header">{{ header }}</div>
    <div class="header-corner"></div>
    <div class="table-item" v-for="(item, index) in table" :key="index">
      <div v-if="item !== 'edit'">
        {{ item }}
      </div>
      <button v-else @click="deleteItem(index)">
        удалить
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'data-table',
  data() {
    return {
      offset: 4,
      headers: ['ID', 'Номер накладной', 'Тип заказа', 'Дата создания'],
    };
  },
  props: {
    data: Array,
    default: () => [],
  },
  computed: {
    table() {
      return this.data.map((e) => [...Object.values(e), 'edit']).flat();
    },
  },
  methods: {
    deleteItem(e) {
      const index = e - this.offset;
      const toRemoveId = this.table[index];
      this.$emit('remove', toRemoveId);
    },
  },
};
</script>
<style scoped lang="scss">
.table {
  gap: 3px;
  display: grid;
  // grid-template-areas:
  //   "h h h h e"
  //   "t t t t e";
  grid-template-columns: min-content;
  grid-template-rows: repeat(1fr);
}
.table-item {
  // grid-area: t;
}
.header {
  // grid-area: h;
  font-weight: 600;
  white-space: nowrap;
  grid-row: 1;
  background: #e6e6e6;
  padding: 11px 62px;
}
.header-corner {
  // grid-area: e;
  grid-row: 1;
  padding: 11px 22px;
  background: #e6e6e6;
}
.item-edit {
  // grid-area: e;
}
</style>
