<template>
    <div class="task-grid">
        <template v-if="tasks.length">
            <Task
                v-for="(task, index) in tasks"
                :key="index"
                :task="task"
                @taskDelete="$emit('taskDelete', $event)"
                @taskStateChange="$emit('taskStateChange', index)"
            />
        </template>
        <p v-else>Sua vida estah em dia!</p>
    </div>
</template>

<script>
import Task from './Task.vue';

export default {
    components: { Task },
    props: {
        tasks: {
            type: Array,
            required: true,
        },
    },
};
</script>

<style scoped>
.task-grid {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
}

.task-grid .task {
    margin: 10px;
}

.no-task {
    color: #aaa;
    font-size: 1.7rem;
}
</style>
