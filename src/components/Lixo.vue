<script lang="ts" setup>
import { inject } from 'vue';

let items = inject<any>('itemData')
const globalData = inject<any>('globalData');

defineProps(['quant', 'price', 'index'])

function handleClick(quant: number, price: number, index: number){
    globalData.globalPrice -= quant * price;
    globalData.globalCount -= quant;
    items.splice(index, 1)
}

</script>

<template>
    <p @click="handleClick(quant, price, index)"><strong>🗑</strong></p>
</template>

<style scoped>
    p {
        background-color: #F7F7F7;
        width: 1.7vw;
        height: 1.7vw;
        border-radius: 0.25vw;
    }

    p:hover {
        cursor: pointer;
        background-color: #d7d7d7;
    }
</style>