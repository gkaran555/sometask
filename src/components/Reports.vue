<template>

  <el-container>  

    <el-header>
      <p>AQUA</p> 
    </el-header>

    <search-reports 
      :myKey = "filterKey"
      :myDir = "filterDir"
      @searchRecords='searchReports'
      @keyChange = "changeKey"
      @dirChange = "changeDir" />

<hr>

    <report-list
      :reports = 'filteredApts' />
  
  </el-container>

</template>

<script>
import _ from 'lodash';
import reportList from './ReportsList.vue';
import SearchReports from './SearchReports.vue';
import axios from 'axios'

export default {
    name: 'Reports',

    components: {
      'report-list': reportList,
      'search-reports': SearchReports
    }, //components
    data() {
        return {
            reports: [],
            searchTerms: '',
            filterKey: 'title',
            filterDir: 'asc'
        };
    },
    methods: {
        fetchIt(){
          axios.get('https://aqua-reports.andagon.com/api/reports')
          .then((response)=> this.reports = response.data)
          .catch((error) => this.errors = error.response.data.errors)
        },

        searchReports: function(terms) {
          this.searchTerms = terms;
        }, //
        changeKey: function(value) {
          this.filterKey = value;
        }, 
        changeDir: function(value) {
          this.filterDir = value;
        }
     
    },

    mounted(){
         this.fetchIt();
    },

    computed: {
        searched: function() {
          return this.reports.filter(function(item) {
            return (
              (item.title.match(this.searchTerms)) ||
              (item.published.match(this.searchTerms)) 
            )
          }.bind(this));
        }, 

        filteredApts: function() {
          return _.orderBy(this.searched, function(item) {
            return item[this.filterKey];
          }.bind(this), this.filterDir);
        } //filteredApts

    } //computed

  }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.el-header {
    background-color: #4b9cd2;
    color: white;
    text-align: center;
    margin-bottom: 15px;
 
  }

</style>
