<template>
    <div @click="$emit('taskStateChange', task)" class="task" :class="classState">
        <span class="close" @click.stop="$emit('taskDelete', task)">x</span>
        <p>{{ task.name }}</p>
    </div>
</template>

<script>
export default {
    props: {
        task: {
            type: Object,
            required: true,
        },
    },
    computed: {
        classState() {
            return {
                pending: this.task.pending,
                done: !this.task.pending,
            };
        },
    },
    methods: {},
};
</script>

<style scoped>
.task {
    position: relative;
    box-sizing: border-box;
    width: 350px;
    height: 150px;
    padding: 10px;
    border-radius: 8px;
    font-size: 2rm;
    display: flex;
    font-weight: 300;
    cursor: pointer;
    user-select: none;
    justify-content: center;
    align-items: center;
}

.pending {
    border-left: 12px solid #b73229;
    background-color: #f44336;
}

.done {
    border-left: 12px solid #0a8f08;
    background-color: #4caf50;
    text-decoration: line-through;
}

.pending .close {
    background-color: #b73229;
}

.done .close {
    background-color: #0a8f08;
}

.close {
    position: absolute;
    top: 10px;
    right: 10px;
    font-size: 0.9rem;
    height: 20px;
    width: 20px;
    border-radius: 10px;
    display: flex;
    justify-content: center;
}
</style>
