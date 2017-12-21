<template>
  <div id="app">
    <div id="excel-table">
      
    </div>

    <result-table></result-table>
  </div>
</template>

<script>
import Vue from 'vue'
import Handsontable from 'handsontable'
import CheckoutButton from './CheckoutButton.vue'
import ResultTable from './ResultTable.vue'
import EventBus from '../EventBus'

export default {
  components : { CheckoutButton, ResultTable },
  mounted() {
    this.createTable();
    EventBus.$on('addToHot', (row) => {
      this.table_data.push(row);
      this.hot.render();
    });
  },
  data : function() {
    return {
      hot : {},
      table_data : [
        [ '2017', '10', '11', '12', '132', '15', '16' ],
        [ '2018', '10', '11', '12', '13', '15', '16' ],
        [ '2019', '10', '11', '12', '16', '15', '16' ],
        [ '2020', '10', '11', '12', '18', '15', '16' ],
        [ '2021', '10', '11', '12', '1', '15', '16' ],
      ],
    }
  },
  methods : {
    createTable : function() {
      var container = document.getElementById('excel-table');
      this.hot = new Handsontable(container, {
        data : this.table_data,
        rowHeaders : false,
        colHeaders : [ 'year', 'Tesla', 'Nissan', 'Toyota', 'Honda', 'Mazda', 'Ford', 'Checkout'],
        columns : [
          { renderer : "text" },
          { renderer : "text" },
          { renderer : "text" },
          { renderer : "text" },
          { renderer : "text" },
          { renderer : "text" },
          { renderer : "text" },
          { renderer : this.buttonRenderer },
        ],
        // filters : true, // 필터기능 존재 여부
        // dropdownMenu : true, // dropdown 메뉴 존재 여부
        afterChange : () => { // 테이블의 내용이 수정된 후 이벤트
        },
      });
    },
    buttonRenderer : function(instance, td, row, col, prop, value, cellProperties) {
      let vm = Vue.extend(CheckoutButton);
      let checkoutButton = new vm();
      
      // checkoutButton 컴포넌트로 데이터 전달
      this.$nextTick(() => {

        checkoutButton._props.index = row;
        checkoutButton._props.table_data = this.table_data;
        checkoutButton._props.hot = this.hot;
        checkoutButton.$mount(td);
      })
    },
  }
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
