<template>
    <td class>
        <button @click="checkout" class="button">Checkout</button>
    </td>
</template>

<script>
import EventBus from '../EventBus'

export default {
    name : "CheckoutButton",
    props : [ 'index', 'row' ],
    methods : {
        checkout : function() {
            EventBus.$emit('getResult', this.row)
            EventBus.$emit('deleteData', this.index)
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