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
        checkin : function () {
            EventBus.$emit('addToHot', this.index)
            EventBus.$emit('deleteAtResult', this.index)
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