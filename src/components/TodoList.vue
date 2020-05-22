<template>
    <div class="list">
        <h3>ToDo List</h3>
        <ul>
            <template v-for="(todo, index) in todos" >
                <li :key="index">
                    <div @click="setNewTodo(todo.description);toggleAreaTodo()"  class="text active">
                        {{`${index + 1}: ${todo.description}`}}
                    </div>
                    <form v-on:submit.prevent="changeTodo(index)" class="text">
                        <input v-model="newTodo">
                        <button class="button-li button-write"  @click="toggleAreaTodo()">
                        <svg viewBox="0 0 512 512" class="icons">
                            <path fill="currentColor" d="M493.26 56.26l-37.51-37.51C443.25 6.25 426.87 0 410.49 0s-32.76 6.25-45.25 18.74l-74.49 74.49L256 127.98 12.85 371.12.15 485.34C-1.45 499.72 9.88 512 23.95 512c.89 0 1.79-.05 2.69-.15l114.14-12.61L384.02 256l34.74-34.74 74.49-74.49c25-25 25-65.52.01-90.51zM118.75 453.39l-67.58 7.46 7.53-67.69 231.24-231.24 31.02-31.02 60.14 60.14-31.02 31.02-231.33 231.33zm340.56-340.57l-44.28 44.28-60.13-60.14 44.28-44.28c4.08-4.08 8.84-4.69 11.31-4.69s7.24.61 11.31 4.69l37.51 37.51c6.24 6.25 6.24 16.4 0 22.63z" class=""></path>
                        </svg>
                        </button>
                    </form>
                    <div class="button-action">
                        <button class="button-li" @click="deleteTodo(index)" title="Удалить задачу из списка дел">
                            <svg viewBox="0 0 352 512" class="icons cancel">
                                <path d="M242.72 256l100.07-100.07c12.28-12.28 12.28-32.19 0-44.48l-22.24-22.24c-12.28-12.28-32.19-12.28-44.48 0L176 189.28 75.93 89.21c-12.28-12.28-32.19-12.28-44.48 0L9.21 111.45c-12.28 12.28-12.28 32.19 0 44.48L109.28 256 9.21 356.07c-12.28 12.28-12.28 32.19 0 44.48l22.24 22.24c12.28 12.28 32.2 12.28 44.48 0L176 322.72l100.07 100.07c12.28 12.28 32.2 12.28 44.48 0l22.24-22.24c12.28-12.28 12.28-32.19 0-44.48L242.72 256z"></path>
                            </svg>
                        </button>
                        <template>
                            <div v-show="todo.completed === true" @click="toggleCheckbox(todo.completed, index)" class="checkbox checkbox-done" title="Отметить задачу как невыполненную">
                                <svg viewBox="0 0 512 512" class="icons icons_checkbox">
                                    <path fill="currentColor" d="M435.848 83.466L172.804 346.51l-96.652-96.652c-4.686-4.686-12.284-4.686-16.971 0l-28.284 28.284c-4.686 4.686-4.686 12.284 0 16.971l133.421 133.421c4.686 4.686 12.284 4.686 16.971 0l299.813-299.813c4.686-4.686 4.686-12.284 0-16.971l-28.284-28.284c-4.686-4.686-12.284-4.686-16.97 0z" class=""></path>
                                </svg>
                            </div>
                            <div v-show="todo.completed === false" @click="toggleCheckbox(todo.completed, index)" class="checkbox checkbox-notdone" title="Отметить задачу как выполненную"> 
                                <svg viewBox="0 0 352 512" class="icons icons_checkbox">
                                    <path path d="M242.72 256l100.07-100.07c12.28-12.28 12.28-32.19 0-44.48l-22.24-22.24c-12.28-12.28-32.19-12.28-44.48 0L176 189.28 75.93 89.21c-12.28-12.28-32.19-12.28-44.48 0L9.21 111.45c-12.28 12.28-12.28 32.19 0 44.48L109.28 256 9.21 356.07c-12.28 12.28-12.28 32.19 0 44.48l22.24 22.24c12.28 12.28 32.2 12.28 44.48 0L176 322.72l100.07 100.07c12.28 12.28 32.2 12.28 44.48 0l22.24-22.24c12.28-12.28 12.28-32.19 0-44.48L242.72 256z"></path>
                                </svg>
                            </div>
                        </template>
                    </div>
                </li>
            </template>
        </ul>
        <form v-on:submit.prevent="addNewTodo" class="addListForm">
            <input v-model="text" placeholder="Поспать, хорошо бы поспать">
            <button class="button-li button-write">
                <svg viewBox="0 0 512 512" class="icons">
                    <path fill="currentColor" d="M493.26 56.26l-37.51-37.51C443.25 6.25 426.87 0 410.49 0s-32.76 6.25-45.25 18.74l-74.49 74.49L256 127.98 12.85 371.12.15 485.34C-1.45 499.72 9.88 512 23.95 512c.89 0 1.79-.05 2.69-.15l114.14-12.61L384.02 256l34.74-34.74 74.49-74.49c25-25 25-65.52.01-90.51zM118.75 453.39l-67.58 7.46 7.53-67.69 231.24-231.24 31.02-31.02 60.14 60.14-31.02 31.02-231.33 231.33zm340.56-340.57l-44.28 44.28-60.13-60.14 44.28-44.28c4.08-4.08 8.84-4.69 11.31-4.69s7.24.61 11.31 4.69l37.51 37.51c6.24 6.25 6.24 16.4 0 22.63z" class=""></path>
                </svg>
            </button>
        </form>

    </div>
</template>

<script>
export default {
    props: ['todos'],
    data() {
        return {
            text: '',
            newTodo: '',
            booleanCheckbox: true,
        }
    },
    methods: {
        deleteTodo(index) {
            this.$emit('delete-todo', index);
        },
        addNewTodo() {
            if (!this.text)alert('Введите текст!')
            if (this.text) {
                const text = this.text;
                this.$emit('add-new-todo', text);
                this.text = '';
            }
        },
        toggleAreaTodo() {
            let li = event.target.closest('li');
            let arrText = li.getElementsByClassName('text');
                for (let item of arrText) {
                    item.classList.toggle('active');
                } 
        },
        changeTodo(index) {
            let text = this.newTodo; 
            console.log;
            this.$emit('change-todo', index, text);
            this.newTodo = '';
        },
        setNewTodo(todo) {
            this.newTodo = todo;
        },
        toggleCheckbox(todoCompleted, index) {
            if (todoCompleted === false) {
                this.$emit('toggle-checkbox', true, index)
            } 
            if (todoCompleted === true) {
                this.$emit('toggle-checkbox', false, index)
            }
        }
    }
}
</script>

<style scope>
    .text{
        display:flex;
        align-items:center;
    }
    .list {
        display: block;
        width: 50%;
        margin: 0 auto;
    }
    .addListForm {
        display: flex;
        width: 50%;
        justify-content: start;
    }
    .addListForm>input {
        min-width:180px;
        height:36px;
    }
    .addListForm>button {
        margin-left:10px;
    }
    .text {
        display: none;
    }
    .active {
        display: flex;
    }
    .button-action {
        width: 90px;
        display: flex;
        justify-content:space-between;
    }
    .button-action>.button-li {
        background: #0072ff;
        box-shadow: none;
        border: 2px solid;
        border-radius: 5px;
        border-color: #0072ff;
    }
    .button-action>.button-li:hover {
        background: #fff;
    }
    .icons {
        width:65%;
        height:65%;
        z-index: 2;
    }
    .icons_checkbox>path {
        fill: #fff;
    }
    .cancel>path {
        fill: #fff;
    }
    .button-action>.button-li:hover .cancel>path {
        fill: #0072ff;
    }
    .checkbox {
        position: relative;
        box-sizing: border-box;
        background: red;
        border: 2px solid;
        border-radius:5px;
        height: 36px;
        width: 36px;
        display: flex;
        justify-content: center;
        align-items: center;
        transition: background .2s;
    }
    .checkbox:hover {
        background: #fff;
    }
    .checkbox-notdone:hover>.icons_checkbox>path  {
        fill: red;
    } 
    .checkbox-done:hover>.icons_checkbox>path  {
        fill: #0dec0d;
    } 
    .checkbox-notdone {
        border-color: red;
    }
    .checkbox-done {
        border-color: #0dec0d;
        background: #0dec0d;
    }

    .button-write {
        border: 3px solid #0072ff;
        position: relative;
        overflow: hidden;
    }
    .button-write::before, 
    .button-write::after {
        position: absolute;
        content: '';
        width:100%;
        height: 100%;
        top:0;
        left:-100%;
        background: rgb(0, 114, 255);
        opacity: 0.5;
        transition: .5s;
    }
    .button-write::after{
        opacity: 1;
        transition-delay: .15s;
    }
    .button-write:hover::before,
    .button-write:hover::after {
        left:0;
    }
    .button-write>.icons path {
        fill: #0072ff;
    }
    .button-write:hover>.icons path {
        fill: #fff;
    }
    h3 {
        text-align: center;
    }
    .button-li {
        box-sizing: border-box;
        height: 36px;
        width: 36px;
        margin-left:10px;
        transition: background .2s;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    ul {
        padding: 0;
    }
    li {
        display: flex;
        justify-content: space-between;
        border: 1px solid rgba(0,0,0,.125);
        padding: 17px 10px;
    }
    input {
        min-width: 100px;
        width: auto;
        height: 36px;
        padding: 0 5px;
    }
</style>