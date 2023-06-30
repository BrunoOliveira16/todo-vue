<script setup>
import { reactive } from 'vue';

    const estado = reactive({
        filtro: 'todas',
        tarefaTemp: '',
        tarefas: [
           {
            titulo: 'Estudar JavaScript',
            finalizada: true,
           },
           {
            titulo: 'Estudar React',
            finalizada: false,
           },
           {
            titulo: 'Estudar Vue',
            finalizada: true,
           },
           {
            titulo: 'Estudar Angular',
            finalizada: false,
           }   
        ]
    })

    const getTarefasPendentes = () => {
        return estado.tarefas.filter(tarefa => !tarefa.finalizada )
    }

    const getTarefasFinalizadas = () => {
        return estado.tarefas.filter(tarefa => tarefa.finalizada )
    }

    const getTarefasFiltradas = () => {
        const { filtro } = estado;

        switch(filtro) {
            case 'pendentes':
                return getTarefasPendentes();
            case 'finalizadas':
                return getTarefasFinalizadas();
            default:
                return estado.tarefas;
        }
    }

    const cadastrarTarefa = () => {
        const novaTarefa = {
            titulo: estado.tarefaTemp,
            finalizada: false,
        }
        estado.tarefas.push(novaTarefa);
        estado.tarefaTemp = '';
    }
</script>

<template>
    <div class="container">
        <header class="p-5 mb-4 mt-4 bg-light rounded-3">
            <h1>Minhas tarefas</h1>
            <p>
                Você possui {{ getTarefasPendentes().length }} tarefas pendentes
            </p>
        </header>
        <form @submit.prevent="cadastrarTarefa">
            <div class="row">
                <div class="col">
                    <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control" required>
                </div>
                <div class="col-md-2">
                    <button class="btn btn-primary">Cadastrar</button>
                </div>
                <div class="col-md-2">
                    <select class="form-control" @change="evento => estado.filtro = evento.target.value">
                        <option value="todas">Todas tarefas</option>
                        <option value="pendentes">Pendentes</option>
                        <option value="finalizadas">Finalizadas</option>
                    </select>
                </div>
            </div>
        </form>
        <ul class="list-group mt-4">
            <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
                <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" type="checkbox" :id="tarefa.titulo">
                <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">
                    {{ tarefa.titulo }}
                </label>
            </li>
        </ul>
    </div>
</template>

<style scoped>
.done {
    text-decoration: line-through;
}
</style>
