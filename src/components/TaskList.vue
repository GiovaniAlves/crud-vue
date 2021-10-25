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
            :task="task"/>
    </ul>

    <p v-else>Nenhuma tarefa criada.</p>

    <TaskSave
        v-if="displayForm"
        @create="createTask"/>

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
            displayForm: false
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
                    this.displayForm = false
                })
        }
    }
}
</script>
