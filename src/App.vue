<template>
  <div class="app">
    <h1>📋 Lista de Tarefas</h1>

    <!-- Mensagem quando não há tarefas -->
    <div v-if="tarefas.length === 0">
      <p>🎉 Parabéns! Você completou todas as tarefas!</p>
    </div>

    <!-- Lista de tarefas usando v-for -->
    <ul v-else>
      <!-- O v-for serve para fazer um loop e criar vários elementos com base em uma lista. -->
      <li v-for="(tarefa, index) in tarefas" :key="index">
        {{ tarefa }}
        <!-- Para cada tarefa (item) da lista tarefas, crie um <li> e me dê também o índice (posição) dessa tarefa. -->
          <!-- tarefa: Representa o item atual da lista, ou seja, cada valor dentro do array tarefas -->
           <!--  index: Representa a posição do item na lista (começa no 0).-->
             <!-- O atributo :key é usado pelo Vue para identificar cada item da lista de forma única. -->
        <button @click="removerTarefa(index)">❌ Remover</button>
      </li>
    </ul>

    <!-- Adicionar nova tarefa -->
    <div class="adicionar-tarefa">
      <input
        type="text"
        v-model="novaTarefa"
        placeholder="Digite uma nova tarefa"
      />
      <!-- v-model sincroniza um valor de uma variavel -->
      <button @click="adicionarTarefa">➕ Adicionar</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// Lista inicial de tarefas
const tarefas = ref(["Estudar Vue.js", "Praticar exercícios de programação"]);
// Armazena a nova tarefa do input
const novaTarefa = ref("");

// Função para adicionar uma tarefa
function adicionarTarefa() {
  if (novaTarefa.value.trim() !== "") { // Verifica se o input não está vazio,
// !==: Verifica se os valores e os tipos são diferentes.
    tarefas.value.push(novaTarefa.value.trim()); // Adiciona a nova tarefa na lista
    novaTarefa.value = ""; // Limpa o campo de texto
  }
}

// Função para remover uma tarefa pelo índice
function removerTarefa(index) {
  tarefas.value.splice(index, 1);// Remove 1 item da lista na posição 'index'
}
</script>

<style>
.app {
  max-width: 600px;
  margin: 20px auto;
  font-family: Arial, sans-serif;
  text-align: center;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  margin: 10px 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #f9f9f9;
  padding: 10px;
  border-radius: 8px;
}

button {
  background: #ff5c5c;
  color: white;
  border: none;
  border-radius: 5px;
  padding: 5px 10px;
  cursor: pointer;
}

button:hover {
  background: #ff1c1c;
}

.adicionar-tarefa input {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.adicionar-tarefa button {
  background: #4caf50;
  color: white;
  border: none;
  border-radius: 5px;
  padding: 8px 15px;
  margin-left: 10px;
  cursor: pointer;
}

.adicionar-tarefa button:hover {
  background: #45a049;
}
</style>
