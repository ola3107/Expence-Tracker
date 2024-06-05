<template>
    <div class="income-expense">
        <div class="income">
            <h4>Credit</h4>
            <p class="money plus">₦{{ credit }}</p>
        </div>
        <div class="expense">
            <h4>Debit</h4>
            <p class="money minus">₦{{ debit }}</p>
        </div>
    </div>
</template>

<script setup>

const props = defineProps({
    credit: {
        type: Number,
        required: true
    },

    debit: {
        type: Number,
        required: true
    }


})




</script>

<style scoped>
    .income-expense {
        display: flex;
        justify-content: space-evenly;
    }

    .income,
    .expense {
        flex: 1;
        padding: 10px;
        text-align: center;
    }

    .income {
        background-color: #f1f8e9;
    }

    .expense {
        background-color: #ffebee;
    }

    h4{
        color: grey;
    }

    .money {
        font-size: 20px;
    }

    .plus {
        color: #2ecc71;
    }

    .minus {
        color: #c0392b;
    }

</style>