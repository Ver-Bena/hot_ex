<template>
  <div id="app">
    <excel-table></excel-table>
    <result-table></result-table>
  </div>
</template>

<script>
import ExcelTable from './ExcelTable.vue'
import ResultTable from './ResultTable.vue'

export default {
  components : { ExcelTable, ResultTable },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  #app > * {
    float: left;
    margin-right: 10px;
  }

  .handsontable td {
    overflow: visible;
    padding: 5px;
  }
</style>
