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

        <tr v-for="(tr_r, i) in result">
            <td v-for="(td_r, j) in tr_r">
                {{td_r}}
            </td>

            <checkin-button></checkin-button>
        </tr>
    </table>
</template>

<script>
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
  created() {
    EventBus.$on("getResult", this.getResultHandler);
  },
  methods : {
    getResultHandler : function(row) {
        this.result.push(row)
        CheckinButton.props.result = row;
    }
  }
}
</script>

<style>
    table, tr, td {
        border: 1px solid black;
        border-collapse: collapse;
    }

    .result-table tr:first-child td {
        background-color: #eee;
    }
</style>