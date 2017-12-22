<template>
    <td>
        <button @click="checkin" class="button">Checkin</button>
    </td>
</template>

<script>
import EventBus from '../EventBus'

export default {
    name : "CheckinButton",
    props : [ 'index', 'result' ],
    methods : {
        checkin : function () { // checkin 버튼을 눌렀을 때
            EventBus.$emit('addToHot', this.result[this.index]) // ExcelTable의 Handsontable에 ResultTable의 해당 열을 추가
            EventBus.$emit('deleteAtResult', this.index) // ResultTable에서 checkin한 열을 삭제
        },
    }
}
</script>

<style>
    .button {
        display: inline-block;
        color: #fff;
        background-color: #4fc08d;
        border: 0;
        border-radius: 5px;
        padding: 10px;
        cursor: pointer;
    }
</style>