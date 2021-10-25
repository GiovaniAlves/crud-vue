<template>
    <h1 class="font-weight-light">Lista de Tarefas </h1>

    <ul class="list-group" v-if="tasks.length > 0">
        <TaskListItem
            v-for="task in tasks"
            :key="task.id"
            :task="task"/>
    </ul>

    <p v-else>Nenhuma tarefa criada.</p>

    <TaskSave />
</template>

<script>
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
            tasks : [
                {id: 1, title: "Aprender JavaScript", concluded: true},
                {id: 2, title: "Aprender Vue", concluded: false},
                {id: 3, title: "Aprender Axios", concluded: true},
            ]
        }
    }
}
</script>
