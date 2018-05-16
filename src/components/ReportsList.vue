<template>
  <ul class="report-list">
    <report-item 
      v-for="(item, i) in reports"
      :report="item"
      :key="i"
    />
  </ul>
</template>

<script>

import reportListItem from './ReportsListItem.vue';

export default {
  name: 'ReportsList',

  props: ['reports'],

  components: {
    'report-item': reportListItem,
  }, //components

} //export

</script>



<style scoped>
  .report-list {
    margin: 0;
    padding: 0;
    list-style-type: none;
    margin: 10px 5%;
    font-size: 1rem;
  }
</style>