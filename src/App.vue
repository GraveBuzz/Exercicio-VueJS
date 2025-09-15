<script setup>
import { reactive } from 'vue';


//cria as um objeto reativo que reagem a mudanças (propriedades)
const estado = reactive({   
  filtro: 'somar',
  numberA: 0,
  numberB: 0,
  resultado: 0,

});

//cria as funções de calculo
const somaNumeros = () => {                 
  return estado.numberA + estado.numberB
}
const subtrairNumeros = () => {
  return estado.numberA - estado.numberB
}
const multiplicarNumeros = () => {
  return estado.numberA * estado.numberB
}
const divideNumeros = () => {
  return estado.numberA / estado.numberB
}


// filtra o select e chama as funções de acordo com o que foi escolhido
const getOperador = () => {
  const { filtro } = estado;

  switch (filtro) {
    case 'somar':
      return somaNumeros;
    case 'subtrair':
      return subtrairNumeros;
    case 'multiplicar':
      return multiplicarNumeros;
    case 'dividir':
      return divideNumeros;
    default:
      return () => 0;

  }
}


// recupera a operação feita no getOperador e coloca no resultado atualizando na interface
const calcular = () => {
    const operacao = getOperador();
    estado.resultado = operacao();
  }

</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light ">
      <h1 class="text-center">Calculadora aritmética</h1>
    </header>
    <form @submit.prevent="calcular">
      <div class="row">
        <select v-model="estado.filtro" class="form-control text-center">
          <option value="somar">Somar (+)</option>
          <option value="subtrair">Subtrair (-)</option>
          <option value="multiplicar">Muliplicar (X)</option>
          <option value="dividir">Dividir(÷)</option>
        </select>
      </div>
      <div class="row">
        <div class="col-md-6">
          <input v-model="estado.numberA" type="number" class="form-control mt-3 mb-3 text-center " placeholder="Coloque o numero">
        </div>
        <div class="col-md-6">
          <input v-model="estado.numberB" type="number" class="form-control mt-3 mb-3 text-center " placeholder="Coloque o numero">
        </div>
      </div>
      <div class="row">
        <button type="submit" class="btn btn-primary">Calcular</button>
      </div>
      <div class="row mt-3 bg-light">
        <h4 class="text-center">O resultado é: {{estado.resultado}}</h4>
      </div>
    </form>
  </div>
</template>

<style scoped>
</style>
