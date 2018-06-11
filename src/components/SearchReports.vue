<template>

<el-input id="SearchApts" placeholder="Search reports" v-model="searchTerm" class="input-with-select">
    <el-select v-model="select" slot="prepend" placeholder="Sort by">

        <el-option  label="title" value="1" >
          <a href="#"  id="title" @click.prevent="requestKeyChange('title')">Title
            <i class="el-icon-check" v-if="myKey==='title'"></i>
          </a>          
        </el-option>

        <el-option label="date" value="2">         
          <a href="#"  id="date" @click.prevent="requestKeyChange('date')">Date
            <i class="el-icon-check" v-if="myKey==='date'"></i>
          </a>
        </el-option>

        <el-option label="asc" value="3">         
          <a href="#"  id="asc" @click="requestDirChange('asc')">Asc
            <i class="el-icon-check" v-if="myDir==='asc'"></i>
          </a>
        </el-option>

        <el-option id="desc" label="desc" value="4">
          <a href="#"  id="desc" @click="requestDirChange('desc')">Desc
            <i class="el-icon-check" v-if="myDir==='desc'"></i>
          </a>
        </el-option>


    </el-select>
    <el-button slot="append" icon="el-icon-search"></el-button>
  </el-input>


</template>

<script>
export default {

  name: 'SearchReports',
  data() {
    return {
      searchTerm: '',
      select: ''
    } //return
  }, //data

  watch: {
    searchTerm: function() {
      this.$emit('searchRecords', this.searchTerm);
    } //searchTerm
  }, //watch

  props: ['myKey', 'myDir'],

  methods: {

    requestKeyChange: function(value) {
      this.$emit('keyChange', value);
    }, //requestKeyChange

    requestDirChange: function(value) {
      this.$emit('dirChange', value);
    } //requestKeyChange

  }

} // export

</script>

<style>
  .el-select .el-input {
    width: 110px;
  }
  .input-with-select .el-input-group__prepend {
    background-color: #fff;
  }
</style>