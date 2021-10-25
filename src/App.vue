<template>
    <div id="app">

        <div class="jumbotron jumbotron-fluid">
            <div class="container">
                <h1 class="display-4">Gerenciador de Tarefas</h1>
                <p class="lead">Usando a biblioteca Axios para fazer chamadas Ajax à uma API REST.</p>
            </div>
        </div>

        <div class="container">
            <TaskList />
        </div>

    </div>
</template>

<script>
import TaskList from "./components/TaskList"
export default {
    components: {TaskList}
}
</script>