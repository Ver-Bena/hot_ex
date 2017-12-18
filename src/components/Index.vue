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

export default {
  components : { CheckoutButton, ResultTable },
  mounted() {
    this.createTable();
  },
  data : function() {
    return {
      hot : {},
      table_data : [
        { a : '10', b : '11', c : '12', d : '132', e : '15', f : '16', },
        { a : '10', b : '11', c : '12', d : '13', e : '15', f : '16', },
        { a : '10', b : '11', c : '12', d : '165', e : '15', f : '16', },
        { a : '10', b : '11', c : '12', d : '18', e : '15', f : '16', },
        { a : '10', b : '11', c : '12', d : '1', e : '15', f : '16', },
      ],
    }
  },
  methods : {
    createTable : function() {
      var container = document.getElementById('excel-table');
      this.hot = new Handsontable(container, {
        data : this.table_data,
        rowHeaders : [ '2017', '2018', '2019', '2020', '2021' ], // 열(row, 가로)의 header 존재 여부
        colHeaders : ['Tesla', 'Nissan', 'Toyota', 'Honda', 'Mazda', 'Ford', 'Checkout'],
        columns : [
          { data : "a", renderer : "text" },
          { data : "b", renderer : "text" },
          { data : "c", renderer : "text" },
          { data : "d", renderer : "text" },
          { data : "e", renderer : "text" },
          { data : "f", renderer : "text" },
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
      
      this.$nextTick(() => {
        checkoutButton._props.index = row;
        checkoutButton._props.table_data = this.table_data;
        checkoutButton._props.hot = this.hot;
        checkoutButton.$mount(td);
      })
    },
    addIt() {
      return "Add It!";
    }
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
