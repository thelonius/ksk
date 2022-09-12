<template>
  <div class="home">
    <FilterBar :orderTypes="orderTypes" @search="searchFilter" @change="filterOrderType"/>
    <Sort @change="sortingDesc = !sortingDesc"/>
    <Table @remove="remove" :data="searchFiltered" />
  </div>
</template>

<script>
// @ is an alias to /src
import Table from '@/components/Table.vue';
import Sort from '@/components/Sort.vue';
import FilterBar from '@/components/Filter.vue';

import { mapState, mapActions } from 'vuex';

export default {
  name: 'HomeView',
  data() {
    return {
      sortingDesc: true,
      selectedValue: '',
      searchValue: '',
    };
  },
  components: {
    Table,
    Sort,
    FilterBar,
  },
  computed: {
    ...mapState({
      cards: (state) => state.cards,
    }),
    dateFormated() {
      return this.cards.map((e) => ({ ...e, creationDate: this.formatDate(e.creationDate) }));
    },
    sortedCards() {
      const sorted = this.dateFormated.slice(0).sort((a, b) => a.number.localeCompare(b.number));

      return this.sortingDesc
        ? sorted
        : sorted.slice(0).reverse();
    },
    filteredCards() {
      return this.selectedValue
        ? this.sortedCards.filter((e) => e.type === this.selectedValue)
        : this.sortedCards;
    },
    orderTypes() {
      return Array(...new Set(this.cards.map((e) => e.type)));
    },
    searchFiltered() {
      return this.filteredCards.filter((e) => e.number.includes(this.searchValue));
    },
  },
  methods: {
    ...mapActions([
      'getCards',
    ]),
    remove(index) {
      // const element = this.cards[index];
      // console.log(index);
      this.$store.commit('delete', index);
    },
    searchFilter(e) {
      this.searchValue = e;
    },
    filterOrderType(e) {
      this.selectedValue = e;
    },
    formatDate: (date) => `${new Date(date).toLocaleDateString('ru')} ${new Date(date).toLocaleTimeString('ru')}`,
  },
  created() {
    this.getCards();
  },
};
</script>
