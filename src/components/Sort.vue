<template>
  <div class="select">
    <label for="select">
      <select id="select" :bind="selectedValue" @change="$emit('change')">
        <option value="asc">номер накладной по возрастанию</option>
        <option value="desc">номер накладной по убыванию</option>
      </select>
    </label>
  </div>
</template>

<script>
export default {
  name: 'select-input',
  data() {
    return {
      selectedValue: 'desc',
    };
  },
  props: {
    // msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss"></style>
