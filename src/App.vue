<template>
  <ag-grid-vue style="width: 700px; height: 300px" class="ag-theme-alpine" :columnDefs="columnDefs" :rowData="rowData"
    :statusBar="statusBar">
  </ag-grid-vue>
</template>

<script>
import "ag-grid-community/dist/styles/ag-grid.css";
import "ag-grid-community/dist/styles/ag-theme-alpine.css";
import { AgGridVue } from "ag-grid-vue3";
import CountStatusBar from "./CountStatusBar.js";
import 'ag-grid-enterprise';
import 'ag-grid-community';
import { LicenseManager } from 'ag-grid-enterprise';

export default {
  name: "App",
  data() {
    return {
      statusBar: null,
      gridOptions: null,
      columnDefs: [
        { headerName: "Make", field: "make" },
        { headerName: "Model", field: "model" },
        { headerName: "Price", field: "price" },
      ],
      rowData: [],
    }
  },
  components: {
    AgGridVue,
    // eslint-disable-next-line vue/no-unused-components
    countStatusBar: CountStatusBar
  },
  beforeMount() {
    //please add the license key to see the issue
    LicenseManager.setLicenseKey("licenseKey");
    this.onGridReady();
  },
  methods: {
    onGridReady(params) {
      console.log("grid ready: ", params);
      this.gridOptions = {
        components: {
          countStatusBar: this.CountStatusBar
        }
      }
    }
  },
  created() {
    this.rowData = [{ make: "Toyota", model: "Celica", price: 35000 },
    { make: "Ford", model: "Mondeo", price: 32000 },
    { make: "Porsche", model: "Boxter", price: 72000 }];
    this.statusBar = {
      statusPanels: [
        { statusPanel: 'countStatusBar', align: "right" },
        {
          statusPanel: 'agTotalAndFilteredRowCountComponent',
          align: 'left',
        },
      ],
    };
  }
};
</script>
