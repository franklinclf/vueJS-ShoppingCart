<script setup lang="ts">
import { provide, reactive } from 'vue';
import { itemData } from './assets/Items';
import Titulo from './components/Titulo.vue'
import Contador from './components/Contador.vue'
import Item from './components/Item.vue';
import Frete from './components/Frete.vue';

function submitAll(){
  if(globalData.globalCount > 0){
    alert("Pedido feito com sucesso!")
  }
  else{
    alert("Adicione itens ao carrinho.")
  }
}

const titulo = 'Carrinho de Compras';
const desc = 'Essa é a lista de itens adicionados ao carrinho:';

const items = reactive(itemData)

const globalData = reactive({
  globalCount: 3,
  globalPrice: 15520,
  globalFrete: 0,
})

provide('globalData', globalData);
provide('itemData', items)
</script>

<template>
  <Titulo :titulo="titulo" :desc="desc"/>
  <Contador/>
  <div class="item-list">
    <div class="item-list-header">
      <p>Produto</p>
      <p>Preço</p>
      <p>Quantidade</p>
      <p>Subtotal</p>
      <p>Excluir</p>
    </div>
    <h2 v-if="globalData.globalCount === 0">O carrinho está vazio.</h2>
    <Item v-for="(item, i) in items" :image="item.image" :name="item.name" :desc="item.desc" :price="item.price" :index="i" :key="item.name"/>
    <div class="checkout">
      <Frete class="div1"/>
      <h2 class="div2">Itens({{ globalData.globalCount }})</h2>
      <h2 class="div3">R$ {{globalData.globalPrice}}</h2>
      <button class="div4" id="submitAll" @click="submitAll">Fazer pedido: <br> R$ {{ globalData.globalPrice + globalData.globalFrete }}</button>
      <h2 class="div5">Frete</h2>
      <h2 class="div6">R$ {{ globalData.globalFrete }}</h2>
    </div>
  </div>
</template>

<style scoped>
.item-list {
  background-color: #FFFFFF;
  box-shadow: 0px 0px 0px 2px #F7F7F7;
  width: 95vw;
  margin: auto;
}

.item-list-header {
  display: grid;
  background-color: #F7F7F7;
  grid-template-columns: 3fr 1fr 1fr 1fr 1fr;
  text-align: center;
}

.checkout {
  width: 95vw;
  display: grid;
  grid-template-columns: 4fr repeat(3, 1fr);
  grid-template-rows: repeat(2, 1fr);
  grid-column-gap: 0px;
  grid-row-gap: 0px;
}
h2 {
  text-align: center;
}

#submitAll {
  background-color: #D7D7D7;
  border-radius: 1vh;
  border: none;
  font-size: large;
  font-weight: bold;
  height: 7vh;
  width: 12vw;
  margin: auto;
}

#submitAll:hover {
  cursor: pointer;
  box-shadow: 0px 0px 1px 2px grey;
}

.div1 { grid-area: 1 / 1 / 3 / 2; }
.div2 { grid-area: 1 / 2 / 2 / 3; }
.div3 { grid-area: 1 / 3 / 2 / 4; }
.div4 { grid-area: 1 / 4 / 3 / 5; }
.div5 { grid-area: 2 / 2 / 3 / 3; }
.div6 { grid-area: 2 / 3 / 3 / 4; }
</style>
