<template>
    <div class="form">
        <h3>Add new transaction</h3>
        <form @submit.prevent="onSubmit">
            <div class="form-control">
                <label for="text">Text</label>
                <input type="text" id="text" v-model="text" placeholder="Enter text..." />
            </div>
            <div class="form-control">
                <label for="amount"
                    >Amount <br />
                    (negative - expense, positive - income)</label
                >
                <input type="text" id="amount" v-model="amount" placeholder="Enter amount..." />
            </div><div class="btn">
                <button class="add-btn">Add transaction</button>
            </div>
        </form>
    </div>
</template>

<script setup>
    import {ref} from 'vue'
    import {useToast} from 'vue-toastification'
    
    const text = ref('')
    const amount = ref('')

    const emit = defineEmits(['transactionSubmitted']);

    const toast = useToast()

    const onSubmit = () => {
        if(!text.value || !amount.value){
            toast.error('both fields are required');
        }else{
            const transactionData = {
                text : text.value,
                amount : parseFloat(amount.value)
            }
            emit('transactionSubmitted', transactionData)
        }

        text.value = ''
        amount.value = ''
        
    }
</script>

<style scoped>
    .form {
        background-color: #f5f5f5;
        padding: 10px;
        border-radius: 10px;
        margin: 5px 0;
        color: #333;
    }

    h3 {
        color: grey;
        text-align: center;
        font-weight: 700;
    }

    .form-control {
        margin: 10px 0;
    }

    label {
        display: block;
        font-weight: 600;
    }

    input {
        width: 100%;
        padding: 8px;
        border-radius: 5px;
        border: 1px solid #ccc;
    }

    .btn{
        display: flex;
        justify-content: center;
    }

    form .btn .add-btn {
        width: 70%;
        padding: 8px;
        border-radius: 5px;
        border: none;
        background-color: #333;
        color: white;
        cursor: pointer;
    }
</style>

