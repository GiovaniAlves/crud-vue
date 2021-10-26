<template>

    <div class="row">
        <div class="col-sm-10">
            <h1 class="font-weight-light">Lista de Tarefas </h1>
        </div>
        <div class="col-sm-2">
            <button
                class="btn btn-primary float-right"
                @click="displayForm = !displayForm">
                    <i class="fa fa-plus mr-2"></i>
                    <span>Criar</span>
            </button>
        </div>
    </div>

    <ul class="list-group" v-if="tasks.length > 0">
        <TaskListItem
            v-for="task in tasks"
            :key="task.id"
            :task="task"
            @edit="selectTaskForEditing"
            @delete="deleteTask"/>
    </ul>

    <p v-else>Nenhuma tarefa criada.</p>

    <TaskSave
        v-if="displayForm"
        :task="selectedTask"
        @create="createTask"
        @edit="editTask"/>

</template>

<script>

import axios from "axios"

import config from "../config/config"
import TaskListItem from "./TaskListItem"
import TaskSave from "./TaskSave"

export default {
    name: "TaskList",
    components: {
        TaskSave,
        TaskListItem
    },
    data() {
        return {
            tasks: [],
            displayForm: false,
            selectedTask: undefined
        }
    },
    created() {
        axios.get(`${config.apiUrl}/tasks`)
            .then((reponse) => {
                this.tasks = reponse.data
            })
    },
    methods: {
        createTask(task){
            axios.post(`${config.apiUrl}/tasks`, task)
                .then((response) => {
                    this.tasks.push(response.data)
                    this.reset()
                })
        },
        deleteTask(task){
            const confirm = window.confirm(`Deseja realmente deletar a tarefa ${task.title}?`)
            if (confirm){
                axios.delete(`${config.apiUrl}/tasks/${task.id}`)
                    .then( () => {
                        const index = this.tasks.findIndex(t => t.id === task.id)
                        this.tasks.splice(index, 1)
                    })
            }
        },
        editTask(task) {
            axios.put(`${config.apiUrl}/tasks/${task.id}`, task)
                .then( response => {
                    const index = this.tasks.findIndex(t => t.id === task.id)
                    this.tasks.splice(index, 1, response.data)
                    this.reset()
                })
        },
        selectTaskForEditing(task){
            this.selectedTask = task
            this.displayForm = true
        },
        reset(){
            this.displayForm = false
            this.selectedTask = undefined
        }
    }
}
</script>
