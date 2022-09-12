<template>
  <div class="filter">
    <h2>Фильтр</h2>
    <h3>Номер накладной</h3>
    <input class="filter-input" type="text" @input="searchInput" />
    <h3>тип заказа</h3>
    <label for="select" value="выберите из списка">
      <select id="select" v-model="selectedValue" @change="emit">
        <option value="">выберите из списка</option>
        <option v-for="(type, index) in orderTypes" :key="index" :value="type">{{ type }}</option>
      </select>
    </label>
  </div>
</template>

<script>
export default {
  name: 'filter-bar',
  data() {
    return {
      initialValue: 'выберите из списка',
      selectedValue: '',
    };
  },
  props: {
    orderTypes: Array,
    default: () => [],
  },
  methods: {
    emit(e) {
      const { value } = e.target;
      this.$emit('change', value);
    },
    searchInput(e) {
      this.$emit('search', e.target.value);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.filter-input {
  // padding: 3px;
}
</style>
