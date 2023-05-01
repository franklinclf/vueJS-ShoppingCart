<script lang='ts' setup>
import { ref, inject, reactive } from 'vue';
import { api } from '../services/api';
let cep = ref('')
let freteStatus = ref('')
let freteData = reactive<any>({});
const globalData = inject<any>('globalData')

async function handleSubmit(cep: string){
    
    try{
        const response = await api.get(`${cep}/json`)
        freteData = response.data
        console.log(freteData)
    }

    catch{
        cep = 'CEP Inválido'
        return;
    }

    if(freteData.erro){
        globalData.globalFrete = 0;
        cep = '';
        freteStatus.value = 'Erro ao verificar o CEP informado.';
    }
    else if(freteData.uf === "RN" || freteData.uf === "CE" || freteData.uf === "PE" || freteData.uf === "MA" || freteData.uf === "SE" || freteData.uf === "PI" || freteData.uf === "PB" || freteData.uf === "BA"){
        globalData.globalFrete = 0;
        cep = '';
        freteStatus.value = freteData.localidade + ' - ' + freteData.uf;
        return;
    }
    else if(freteData.uf == "RR" || freteData.uf === "RO" || freteData.uf === "PA" || freteData.uf === "AC" || freteData.uf === "PA" || freteData.uf === "AP" || freteData.uf === "MT"){
        globalData.globalFrete = 50;
        cep = '';
        freteStatus.value = freteData.localidade + ' - ' + freteData.uf;
        return
    }
    else{
        globalData.globalFrete = 35;
        cep = '';
        freteStatus.value = freteData.localidade + ' - ' + freteData.uf;
        return
    }

}

</script>

<template>
    <div class="container">
        <h2>Calcule o frete:</h2>
        <form v-on:submit.prevent="handleSubmit(cep)">
            <label for="CEP"><strong>CEP: </strong>
                <input placeholder='Insira um CEP válido' v-model="cep" name="CEP" id="CEP" pattern="[0-9]{5}[\-]?[0-9]{3}" required/>
            </label>
            <input type="submit" value="Calcular">
        </form>
        <p>{{ freteStatus }}</p>
    </div>
</template>

<style scoped>
    .container {
        padding: 2vw;
    }
</style>