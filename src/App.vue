<template>
    <div id="app">
        <h1>Progresso</h1>
        <TaskProgress :progress="progress" />
        <CreateTask @taskAdd="taskAdd" />
        <h1>Tarefas</h1>
        <TaskGrid :tasks="tasks" @taskDelete="taskDelete" @taskStateChange="toogleTaskState" />
    </div>
</template>

<script>
import TaskProgress from './components/TaskProgress.vue';
import CreateTask from './components/CreateTask.vue';
import TaskGrid from './components/TaskGrid.vue';

export default {
    components: { TaskProgress, TaskGrid, CreateTask },
    data() {
        return {
            tasks: [],
        };
    },
    watch: {
        tasks: {
            deep: true,
            handler() {
                localStorage.setItem('tasks', JSON.stringify(this.tasks));
            },
        },
    },
    computed: {
        progress() {
            const total = this.tasks.length;

            const totalDone = this.tasks.filter((e) => !e.pending).length;

            return Math.round((totalDone / total) * 100) || 0;
        },
    },
    methods: {
        taskAdd(task) {
            const sameName = (e) => e.name === task.name;

            const isRealyNew = this.tasks.filter(sameName).length === 0;

            if (isRealyNew) {
                this.tasks.push({
                    name: task.name,
                    pending: task.pending || true,
                });
            }
        },
        taskDelete(task) {
            const index = this.tasks.indexOf(task);

            if (index >= 0) this.tasks.splice(index, 1);
        },
        toogleTaskState(index) {
            this.tasks[index].pending = !this.tasks[index].pending;
        },
    },
    created() {
        // const data_tasks = [
        //     { name: 'dancar', pending: true },
        //     { name: 'caminhar', pending: true },
        //     { name: 'pular', pending: false },
        // ];

        // this.tasks = data_tasks;

        const json = localStorage.getItem('tasks');

        this.tasks = JSON.parse(json) || [];
    },
};
</script>

<style>
body {
    font-family: 'Lato', sans-serif;
    background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
    color: #fff;
}

#app {
    display: flex;
    flex: 1;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

#app h1 {
    margin-bottom: 5px;
    font-weight: 300;
    font-size: 3rem;
}
</style>
