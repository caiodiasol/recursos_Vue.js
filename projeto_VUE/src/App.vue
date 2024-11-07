<script setup>
import { reactive } from "vue";

const nome = 'Caio'
const meuObjeto = {
  nome: 'Caio',
  filmeFavorito: 'O Astronauta'
}

function dizOlá(nome) {
  return `${nome} diz olá`;
}

const renderizandoImagemCogu = 'https://img.freepik.com/free-vector/hand-drawn-butterfly-illustration_52683-114320.jpg?t=st=1730929513~exp=1730933113~hmac=d9f1c84dfa0638e88db002289f9837d27d876070d2fc205f7c30096b02459e1b&w=996';
const renderizandoImagemPaz = 'https://img.freepik.com/free-vector/hand-drawn-retro-peace-symbol-illustration_52683-114329.jpg?t=st=1731001336~exp=1731004936~hmac=6468657e34a94acd8ddb6f8998272ab0af5f020174c1cab03e6edea0bbbc9460&w=826';


const botaoEstaDesabilitado = false

const gostaDeCogus = true 
const gostaDaPaz = false

const estaAutorizado = true

// let contador = 0;
const estado = reactive({
  contador: 0,
  email:'',
  saldo: 5000,
  transferindo: 0,
  nomes : ['Caio', 'Paulo', 'Joana', 'Vitoria', 'Luna'],
  nomeAInserir: '',
})

function incrementar(){
  estado.contador++;
}

function decrementar(){
  estado.contador--;
}


function alteraEmail(evento){
  estado.email = evento.target.value;
}

function mostraSaldoFuturo(){
  const { saldo, transferindo } = estado;
  return saldo - transferindo;
}

function validaValorDeTransferencia(){
  const { saldo, transferindo } = estado;
  return saldo >= transferindo;
}

function cadastraNome(){
  if (estado.nomeAInserir.length >= 3){
    estado.nomes.push(estado.nomeAInserir)
  } else {
    alert('Gigite mais caracteres')
  }
}


</script>

<template>
  <h1>{{ dizOlá(nome) }}</h1>
  <img v-if="gostaDeCogus" :src="renderizandoImagemCogu" alt="template cogus">
  <img v-else-if="gostaDaPaz" :src="renderizandoImagemPaz" alt="template da paz">
  <h2 v-else>Não curte a vida leve</h2>

  <h1 v-if="estaAutorizado">Bem-vindo!</h1>
  <h1 v-else>Não possui acesso</h1>

  <button :disabled="botaoEstaDesabilitado" >Enviar mensagem</button>

  <br />
  <hr />
  
  {{ estado.contador }}

  <button @click="incrementar" type="button">+</button>
  <button @click="decrementar" type="button">-</button>

  <br />
  <hr />

  {{ estado.email }}

  <input type="email" @keyup="alteraEmail">

  <br />
  <hr />

  Saldo: {{ estado.saldo }} <br />
  Transferindo: {{ estado.transferindo }} <br />
  Saldo após tranferência: {{ mostraSaldoFuturo() }} <br />
  <input class="campo" :class="{ invalido: !validaValorDeTransferencia() }" @keyup="evento => estado.transferindo = evento.target.value" type="number" placeholder="Quantia para transferir" />
  <button v-if="validaValorDeTransferencia()">Transferir</button>
  <span v-else>Valor maior que o saldo</span>

  <br />
  <hr />

  <ul>
    <li v-for="nome in estado.nomes">
      {{ nome }}
    </li>
  </ul>
  <input @keyup="evento => estado.nomeAInserir = evento.target.value" type="text" placeholder="Digite um novo nome">
  <button @click="cadastraNome()" type="button">Cadastrar Nome</button>

  <h3 v-for="nome in estado.nomes">{{ nome }}</h3>


</template>


<style scoped>

img{
  max-width: 300px;
}

.invalido{
  outline-color: red ;
  border-color: red;
}

.campo{
  border: 3px solid black ;
}

</style>
