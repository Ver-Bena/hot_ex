<template>
    <table class="result-table">
        <tr>
          <td>year</td>
          <td>Tesla</td>
          <td>Nissan</td>  
          <td>Toyota</td>
          <td>Honda</td>
          <td>Mazda</td>
          <td>Fod</td>
          <td>Checkin</td>
        </tr>

        <tr v-for="tr_r in result">
            <td v-for="td_r in tr_r">
                {{td_r}}
            </td>
            
            <td class="checkin-button">

            </td>
        </tr>
    </table>
</template>

<script>
import Vue from 'vue'
import CheckinButton from './CheckinButton.vue'
import EventBus from '../EventBus';

export default {
  name : "ResultTable",
  components : { CheckinButton },
  data() {
      return {
        result : [],
      }
  },
  mounted() {
    EventBus.$on("getResult", this.getResultHandler) // checkout 버튼을 눌렀을 때 EventBus로 해당 row를 전달받는다
    EventBus.$on("deleteAtResult", this.deleteAtResultHandler) // checkin 버튼을 눌렀을 때 EventBus로 해당 row의 index를 전달받는다
  },
  methods : {
    getResultHandler : function(row) {
        let vm = Vue.extend(CheckinButton)
        let checkinButton = new vm()

        this.result.push(row) // result 배열에 push

        this.$nextTick(() => {
            checkinButton._props.index = this.result.indexOf(row); // 
            checkinButton._props.result = this.result;
            checkinButton.$mount('.checkin-button')
        })
    },
    deleteAtResultHandler : function(index) {
        console.log("삭제!", index);
        this.result.splice(index, 1)
    }
  }
}
</script>

<style>
    .result-table, .result-table tr, .result-table td {
        border: 1px solid #ccc;
        border-collapse: collapse;
    }

    .result-table td {
        padding: 2px 4px;
    }

    .result-table tr:first-child td {
        background-color: #eee;
    }
</style>