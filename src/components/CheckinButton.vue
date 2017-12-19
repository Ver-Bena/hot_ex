<template>
    <td class>
        <button @click="checkin" class="button">Checkin</button>
    </td>
</template>

<script>
import EventBus from '../EventBus'

export default {
    name : "CheckinButton",
    props : [ 'result' ],
    methods : {
        checkin : function () {
            // this.addToHot();
            console.log(this.result)
        },
        addToHot : function() {
            EventBus.$emit('checkinData', this.result);
        },
        deleteDataHandler : function(index) {
            this.table_data.splice(index, 1)
            this.hot.render()
        }
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