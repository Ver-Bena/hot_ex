<template>
    <td class>
        <button @click="checkout" class="button">Checkout</button>
    </td>
</template>

<script>
import EventBus from '../EventBus'

export default {
    name : "CheckoutButton",
    props : [ 'index', 'table_data', 'hot' ],
    methods : {
        checkout : function() {    
            this.getDataHandler(this.index)
            this.deleteDataHandler(this.index)
        },
        getDataHandler : function(index) {
            EventBus.$emit('getResult', this.table_data[index]);
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