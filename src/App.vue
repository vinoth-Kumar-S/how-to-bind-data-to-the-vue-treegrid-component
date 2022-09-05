<template>
  <ejs-button :onclick="btnClick" cssClass="btn">Bind Data</ejs-button>
  <ejs-treegrid :dataSource="data"
    ref="treeGridObj"
    idMapping="TaskID"
    parentIdMapping="ParentItem"
    hasChildMapping="isParent"
    :treeColumnIndex="1">
    <e-columns>
      <e-column field="TaskID" headerText="Task ID" width="70" textAlign="Right"></e-column>
      <e-column field='TaskName' headerText='Task Name' width='200'></e-column>
      <e-column field='StartDate' headerText='Start Date' width='90' format="yMd" textAlign='Right'></e-column>
      <e-column field='EndDate' headerText='End Date' width='90' format="yMd" textAlign='Right'></e-column>
      <e-column field='Duration' headerText='Duration' width='80' textAlign='Right'></e-column>
      <e-column field='Progress' headerText='Progress' width='80' textAlign='Right'></e-column>
      <e-column field='Priority' headerText='Priority' width='90'></e-column>
    </e-columns>
  </ejs-treegrid>
</template>

<script>
import {TreeGridComponent, ColumnsDirective, ColumnDirective} from '@syncfusion/ej2-vue-treegrid';
// import {projectData} from './data.js';
// import {DataManager, WebApiAdaptor} from '@syncfusion/ej2-data';
import {ButtonComponent} from '@syncfusion/ej2-vue-buttons';
import {Ajax} from '@syncfusion/ej2-base';
export default {
  name: 'App',
  components: {
    'ejs-treegrid': TreeGridComponent,
    'e-columns': ColumnsDirective,
    'e-column': ColumnDirective,
    'ejs-button': ButtonComponent
  },
  data:()=>{
    // let service_URI = "https://ej2services.syncfusion.com/production/web-services/api/SelfReferenceData";
    return{
      // data: new DataManager({
      //   url: service_URI,
      //   adaptor: new WebApiAdaptor(),
      //   crossDomain: true
      // })
    }
  },
  methods:{
    btnClick: function(){
      let treeGrid = this.$refs.treeGridObj.ej2Instances; //tree grid instance
      let ajax = new Ajax("https://ej2services.syncfusion.com/production/web-services/api/SelfReferenceData", "GET");
      treeGrid.showSpinner();
      ajax.send();
      ajax.onSuccess = function (result) {
        treeGrid.hideSpinner();
        treeGrid.dataSource= JSON.parse(result);
      }
    }
  }
}
</script>

<style>
  @import "../node_modules/@syncfusion/ej2-base/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-calendars/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-dropdowns/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-inputs/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-navigations/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-popups/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-vue-grids/styles/material.css";
  @import "../node_modules/@syncfusion/ej2-vue-treegrid/styles/material.css";

  .btn{
    margin: 1%;
  }
</style>
