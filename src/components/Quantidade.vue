<script lang='ts' setup>
defineProps(['quant', 'price'])

</script>

<template>
    <div class="quant-container">
        <div class="minus" @click="$emit('op', 0, price)">-</div>
        <div class="quant">{{ quant }}</div>
        <div class="plus" @click="$emit('op', 1, price)">+</div>
    </div>
</template>

<style scope>

.quant-container {
    user-select: none;
    display: grid;
    margin: auto;
    width: 5vw;
    height: 1.7vw;
    border-radius: 0.25vw;
    background-color: #F7F7F7;
    grid-template-columns: 1fr 1fr 1fr;
}

.minus, .plus {
    border-radius: 0.25vw;
}

.minus:hover, .plus:hover{
    cursor: pointer;
    background-color: #d7d7d7;
}

</style>