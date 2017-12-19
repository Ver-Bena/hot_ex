<template>
    <table class="result-table">
        <tr>
          <td></td>
          <td>Tesla</td>
          <td>Nissan</td>  
          <td>Toyota</td>
          <td>Honda</td>
          <td>Mazda</td>
          <td>Fod</td>
        </tr>

        <!-- <tr v-for="(c, index) in car">
            <td>{{c.name}}</td>
        </tr> -->
    </table>
</template>

<script>
import EventBus from '../EventBus';

export default {
  name : "ResultTable",
  data() {
      return {
        result : [],
      }
  },
  mounted() {
      EventBus.$on("deletedData", this.deletedDataHandler);
  },
  methods : {
    deletedDataHandler : function(text) {
        //  console.log(text);
        this.result.push(text)
        console.log(this.result)
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