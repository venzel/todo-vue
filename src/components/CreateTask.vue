<template>
    <div class="create-task">
        <input v-model="name" @keydown.enter="add" type="text" class="form-element" placeholder="Nova tarefa" />
        <button class="form-element" @click="add">+</button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            name: '',
        };
    },
    methods: {
        validate(e) {
            const status = {
                error: false,
                message: '',
            };

            if (!e) {
                status['error'] = true;
                status['message'] = 'Preencha o campo corretamente!';
            }

            return status;
        },
        add() {
            const { error, message } = this.validate(this.name);

            if (error) {
                alert(message);
                return;
            }

            this.$emit('taskAdd', { name: this.name });

            this.name = '';
        },
    },
};
</script>

<style scoped>
.create-task {
    margin: 35px;
}

.form-element {
    outline: none;
    font-size: 2rem;
    border: 1px solid #fff;
    padding: 5px 10px 8px;
    color: #fff;
}

input.form-element {
    width: 500px;
    background: #fff2;
    border-top-left-radius: 8px;
    border-bottom-left-radius: 8px;
}

button.form-element {
    border-left: none;
    background-color: #2196d3;
    border-top-right-radius: 8px;
    border-bottom-right-radius: 8px;
}
</style>
