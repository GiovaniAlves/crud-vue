<template>
    <li class="list-group-item d-flex">
        <span>{{ task.title }}</span>
        <span class="espacar"></span>
        <button
            class="btn btn-sm mr-4"
            :class="cssClass"
            :title="completedButtonTitle"
            @click="conclude">
                <i class="fa fa-check"></i>
        </button>
        <button
            class="btn btn-primary btn-sm mr-1"
            title="Editar"
            @click="$emit('edit', task)">
                <i class="fa fa-pencil-alt"></i>
        </button>
        <button
            class="btn btn-danger btn-sm"
            title="Deletar"
            @click="$emit('delete', task)">
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
        cssClass() {
            return {
                'btn-secondary': !this.task.concluded,
                'btn-success': this.task.concluded
            }
        },
        completedButtonTitle() {
            return this.task.concluded ? 'Refazer tarefa' : 'Concluir tarefa'
        }
    },
    methods: {
        conclude() {
            this.$emit('conclude', Object.assign({}, this.task, {concluded: !this.task.concluded}))
        }
    }
}
</script>

<style scoped>

    .espacar {
        flex: 1 1 auto;
    }

</style>