<template>
    <div class="mt-4">
        <hr>
        <h2 class="font-weight-light">Salvar Tarefa</h2>

        <form @submit.prevent="save">
            <div class="row">
                <div :class="classColumn">
                    <div class="form-group">
                        <label>Título</label>
                        <input
                            type="text"
                            class="form-control"
                            placeholder="Título da tarefa"
                            v-model="taskLocal.title">
                    </div>
                </div>
                <div class="col-sm-2" v-if="task">
                    <label>Tarefa Concluída?</label>
                    <button class="btn btn-secondary btn-sm d-block">
                        <i class="fa fa-check"></i>
                    </button>
                </div>
            </div>

            <button type="submit" class="btn btn-primary">Salvar</button>
        </form>
    </div>
</template>

<script>

export default {
    name: "TaskSave",
    props: {
        task: {
            type: Object,
            default: undefined
        }
    },
    data() {
        return {
            taskLocal: Object.assign(
                {},
                {title: '', concluded: false},
                this.task)
        }
    },
    computed: {
        classColumn() {
            return this.task ? 'col-sm-10' : 'col-sm-12'
        }
    },
    methods: {
        save(){
            this.$emit('create', this.taskLocal)
            this.taskLocal = {title: '', concluded: false}
        }
    }
}
</script>

<style scoped>

</style>