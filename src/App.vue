<script setup>
import { reactive } from 'vue';

const nome = "yuri vidal"
const meuObjeto = {
  nome: "leticia",
  filmeFavorito: "terror"
}

function dizOla(nome) {
  return `${nome} diz oi`;
}

const endereçoDaImagem = "https://s2-g1.glbimg.com/P6-Gw0KmcFCO3ZHlSX06vVGdB0Y=/0x0:6000x4000/924x0/smart/filters:strip_icc()/i.s3.glbimg.com/v1/AUTH_59edd422c0c84a879bd37670ae4f538a/internal_photos/bs/2022/m/U/1UvLUASZAevRCb1TBygQ/the-batman-robert-pattinson.jpeg"
const imagemSuperman = "https://veja.abril.com.br/wp-content/uploads/2016/06/cinema-homem-de-aco-super-homem-20110823-0002-original1.jpeg?quality=90&strip=info&w=680&h=453&crop=1"
const botaoEstaDesabilitado = false

const gostaDoBatman = false
const gostaDoSuperman = false

const estaAutorizado = false

// let contador = 0 
const estado = reactive({
  contar: 0,
  email: '',
  saldo: 5000,
  transferindo: 0,
  nomes: ['Yuri', 'Leticia', 'Matheus', 'Julia'],
  nomeAInserir: '',
})

function incrementar() {
  estado.contar++;
} 

function decrementar() {
  estado.contar--;
} 

function alteraEmail(evento) {
  estado.email = (evento.target.value);
}

function mostraSaldoFuturo() {
  const { saldo, transferindo } = estado;
  return saldo - transferindo;
}

function validaValorDeTransferencia() {
  const { saldo, transferindo } = estado;
  return saldo >= transferindo;
}

const nomes = ['Yuri', 'Leticia', 'Matheus', 'Julia'];

function cadastraNome() {
  if (estado.nomeAInserir.length >= 3) {
    estado.nomes.push(estado.nomeAInserir)
  } else {
    alert("Digite mais caracteres")
  }
}

</script>

<template>
<h1>{{ dizOla("paulo") }}</h1>
<img v-if="gostaDoBatman" :src="endereçoDaImagem" alt="">
<img v-else-if="gostaDoSuperman" :src="imagemSuperman" alt="">
<h2 v-else>Não curte herios da DC</h2>

<h1 v-if="estaAutorizado">Bem-Vindo</h1>
<h1 v-else>Não possui acesso</h1>

<button :disabled="!botaoEstaDesabilitado">enviar mensagem</button>

<br />
<hr />

{{ estado.contar }}

<button @click="incrementar" type="button">+</button>
<button @click="decrementar" type="button">-</button>

<br />
<hr />

{{ estado.email }}

<input type="email" @keyup="alteraEmail">

<br />
<hr />

Saldo: {{ estado.saldo }} <br>
Tranferindo: {{ estado.transferindo }} <br>
Saldo depois da transferencia: {{ mostraSaldoFuturo() }}

<input :class="{ invalido: !validaValorDeTransferencia() }" @keyup="evento => estado.transferindo = evento.target.value" type="number" placeholder="Quantia para tranferir">
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
<button @click="cadastraNome" type="button">Cadastrar nome</button>

  <h3 v-for="nome in estado.nomes">{{ nome }}</h3>
</template>


<style scoped>
img {
  max-width: 200px;
}

.invalido {
  outline-color: red;
  border-color: red;
}
</style>
