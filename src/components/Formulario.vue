<script setup>
    const props = defineProps(['cadastrarTarefa', 'tarefaTemp', 'trocarFiltro', 'editarTarefaTemp' ])
</script>

<template>
    <form @submit.prevent="props.cadastrarTarefa">
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTemp" @change="props.editarTarefaTemp" type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control" required>
            </div>
            <div class="col-md-2 mt-2 mt-lg-0 mt-md-0">
                <button class="btn btn-primary w-100">Cadastrar</button>
            </div>
            <div class="col-md-2 mt-2 mt-lg-0 mt-md-0">
                <select class="form-control" @change="props.trocarFiltro">
                    <option value="todas">Todas tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>