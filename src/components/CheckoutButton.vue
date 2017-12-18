<template>
    <td class>
        <button @click="checkout" class="button">Checkout</button>
    </td>
</template>

<script>
    export default {
        name : "CheckoutButton",
        props : [ 'index', 'hot', 'table_data' ],
        data() {
            return {
            }
        },
        methods : {
            checkout : function() {
                console.log(this.hot);

                this.table_data.splice(this.index, 1);
                this.hot.render();

                
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