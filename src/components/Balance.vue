<template>
    <div class="container">
        <h4>Your Balance</h4>
        <h1>₦{{ total }}</h1>
    </div>
</template>

<script setup>
    import {defineProps} from 'vue'

    const props = defineProps({
        total: {
            type: Number,
            required: true,
        }
    })
</script>

<style scoped>
    .container {
    background-color: #f5f5f5;
    padding: 10px 20px;
    border-radius: 10px;
    margin: 20px 0;
    color: #333;
  }
</style>