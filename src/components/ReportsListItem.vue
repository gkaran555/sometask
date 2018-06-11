<template>
  <li>

    <div class="media" >
      <div class="media-left">
        <a href="#" @click="dialogopen(report)">
          <img class="media-object" :src="imagebase64Source" alt="...">
        </a>
      </div>
      <div class="media-body">
        <h4 class="media-heading" ref="Name">{{report.title}}</h4> 

        <span class=""><i class="el-icon-date"></i> {{this.formattedDate}}</span>
        
        <p>{{report.description}}</p>
               
        <a :href="dllink" target="_blank" download='report.pdf' class="ccc"><i class="el-icon-download"></i> Export as PDF</a>
      </div>
   </div>




    <el-dialog
      :visible.sync="dialogVisible"
      width="90%"
      >
      <img class="novaslika" :src="newimage" alt="...">
      
    </el-dialog>

   <hr>

  </li>
  


</template>

<script>

import moment from 'moment';

export default {
  name: 'ReportsListItem',
  props: ['report'],
  
  data () {
    return {
      imagebase64Source: this.report.thumbnailURL,
      dialogVisible: false,
      reportimage: [],
      newimage: [],
      dllink: this.report.pdfURL
    }
  },
  computed: {
    formattedDate: function() {
      return moment(new Date(this.report.published)).format('MM-DD-YY, h:mm a');
    } //formattedDate
  }, //computed

  methods: {
    dialogopen: function(some) {
      this.reportimage = some;
      this.newimage = this.reportimage.thumbnailURL,
      this.dialogVisible = true;
    }

  }
 

} //default

</script>

<style scoped>

.media {
  display: flex;
}
.media-left {
  border: 1px solid #4b9cd2;
  margin-right: 20px;
}
.media-body {
  display: flex;
  flex-direction: column;
  text-align: left;
}

.modal-body img{
  width: 100%;

}
.novaslika {
  width: 100%;
}
.ccc {
  font-size: 15px;
  margin-bottom: 7px;
  text-decoration: none;
  color: red;

}

@media only screen and (max-width: 650px) {
    .media {
      display: flex;
      flex-wrap: wrap;
    }
    .media-left {
      width: 100%;
    }
}

</style>