<template>
    <li class="list-group-item d-flex">
        <span>{{ task.title }}</span>
        <span class="espacar"></span>
        <button class="btn btn-sm mr-4" :class="classCss" :title="titleButtonConcluded">
            <i class="fa fa-check"></i>
        </button>
        <button class="btn btn-primary btn-sm mr-1" title="Editar">
            <i class="fa fa-pencil-alt"></i>
        </button>
        <button class="btn btn-danger btn-sm" title="Deletar">
            <i class="fa fa-trash"></i>
        </button>
    </li>
</template>

<script>
export default {
    name: "TaskListItem",
    props: {
        task: {
            type: Object,
            required: true
        }
    },
    computed: {
        classCss() {
            return {
                'btn-secondary': !this.task.concluded,
                'btn-success': this.task.concluded
            }
        },
        titleButtonConcluded() {
            return this.task.concluded ? 'Refazer tarefa' : 'Concluir tarefa'
        }
    }
}
</script>

<style scoped>

    .espacar {
        flex: 1 1 auto;
    }

</style>