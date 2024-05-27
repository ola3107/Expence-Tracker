<template>
    <div class="transactions">
        <h3>Transactions</h3>
        <ul class="list">
            <li v-for="transaction in transactions" :key="transaction.id" :class="transaction.amount < 0? 'minus' : 'plus'" v-if="transactions.length">
                {{ transaction.text }} <span>₦{{ transaction.amount }}</span><button class="delete-btn" @click="deleteTransaction(transaction.id)">X</button>
            </li>

            <li v-else class="no-transaction"> No Transaction Done</li>
        </ul>
    </div>
</template>

<script setup>
    import {defineProps, defineEmits} from 'vue'

    const props = defineProps({
        transactions:{
            type: Array,
            required: true
        }
    })

    const emit = defineEmits(['transactionDeleted']);


    const deleteTransaction = (id) => {
        emit('transactionDeleted', id)
    }
    
</script>


<style scoped>

    h3{
        color: grey;
        text-align: center;
        font-weight: 700;
    }

    .transactions {
        background-color: #f5f5f5;
        padding: 10px;
        border-radius: 10px ;
        margin: 20px 0;
        color: #333;
        
    }

    .list {
        list-style-type: none;
        padding: 0;
        height: 150px;
        overflow: hidden;
        overflow-y: scroll;
    }

    .list li {
        display: flex;
        justify-content: space-between;
        padding: 10px;
        border-bottom: 1px solid #ccc;
        font-weight: 600;
    }

    .list li.no-transaction {
       display: flex;
       justify-content: center;
       align-items: center;
       border: 1px solid;
    }

    .list li.minus {
        color: #c0392b;
    }

    .list li.plus {
        color: #2ecc71;
    }

    .delete-btn {
        background-color: #c0392b;
        color: white;
        border: none;
        padding: 5px 10px;
        border-radius: 5px;
        cursor: pointer;
        opacity: 0;
        transition: opacity 0.3s ease;
    }

    .list li:hover .delete-btn {
        opacity: 1;
    }

    @media screen and (max-width: 1045px) {
        .delete-btn {
            opacity: 1;
        }
    }

</style>