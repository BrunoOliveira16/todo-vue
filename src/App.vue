<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaTarefas from './components/ListaTarefas.vue';

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
        <Cabecalho 
            :tarefas-pendentes="getTarefasPendentes().length" 
        />
        <Formulario
            :tarefa-temp="estado.tarefaTemp"
            :editar-tarefa-temp="evento => estado.tarefaTemp = evento.target.value"
            :cadastrar-tarefa="cadastrarTarefa"
            :trocar-filtro="evento => estado.filtro = evento.target.value"
        />
        <ListaTarefas 
            :tarefas="getTarefasFiltradas()"
        />
    </div>
</template>


