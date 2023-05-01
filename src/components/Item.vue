<script lang='ts' setup>
import { ref, computed, inject } from 'vue';
import Quantidade from './Quantidade.vue';
import Lixo from './Lixo.vue';

const props = defineProps(['image', 'name', 'desc', 'price', 'index']);
const globalData = inject<any>('globalData');
const quant = ref(1);
const subtotal = computed(() =>{ return (quant.value * props.price)})

function clickHandler(op: number, price: number){
    if(op == 1){
        quant.value++;
        globalData.globalCount++;
        globalData.globalPrice += price;
    }
    else{
        if(quant.value === 1){
        return;
    }
        quant.value--;
        globalData.globalCount--;
        globalData.globalPrice -= price;
    }
}

</script>

<template>
    <div class="item-container">
        <div class="info-container">
            <img :src="image"/>
            <p><strong>{{ name }}</strong><br>{{ desc }}</p>
        </div>
        <p>R$ {{ price }}</p>

        <Quantidade :quant="quant" :price="price" @op="clickHandler"/>

        <p>R$ {{ subtotal }}</p>

        <Lixo :quant="quant" :price="price" :index="index"/>
    </div>
<hr>
</template>

<style scope>

img {
    background-color: white;
    width: 7vw;
    height: 7vw;
    object-fit: contain;
    margin: 1vw;
    float: left;
}

.item-container {
    display: grid;
    grid-template-columns: 3fr 1fr 1fr 1fr 1fr;
    text-align: center;
    align-items: baseline;
    place-content: center;
}

.info-container p{
    margin-top: 3.5vh;
    text-align: left;
}
p {
    margin: auto;
}

</style>