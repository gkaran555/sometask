<template>
  <li class="media">

    <div class="media" >
      <div class="media-left">
        <a href="#" @click="dialogopen(report)">
          <img class="media-object" :src="imagebase64Source" alt="...">
        </a>
      </div>
      <div class="media-body">
        <h4 class="media-heading" ref="Name">{{report.title}}</h4>
        <p>{{report.description}}</p>
        <span class="ccc">{{this.formattedDate}}</span>
        <a :href="dllink" download='report.pdf' class="ccc">Export as PDF</a>
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

.modal-body img{
  width: 100%;

}
.novaslika {
  width: 100%;
}
.ccc {
  font-size: 15px;
  margin-bottom: 7px;
}
</style>