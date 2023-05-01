<script lang="ts" setup>
import { inject } from 'vue';

const globalData = inject<any>('globalData');
</script>

<template>
    <p v-if="globalData.globalCount === 1 && globalData.globalCount !== 0">Você tem 1 item no carrinho.</p>
    <p v-else>Você tem {{ globalData.globalCount }} itens no carrinho.</p>
</template>

