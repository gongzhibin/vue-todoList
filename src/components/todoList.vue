<template>
    <div class="todo-list">
        <h1>Todo Lsit</h1>
        <div class="add-todo">
            <input class="form-control" type="text" @keydown.enter="addTodoItem" v-model="todoInput" placeholder="Please enter your todo">
            <button class="btn btn-default" @click="addTodoItem">add todo</button>
        </div>
        <div v-for="(todoItem,index) in todoList" :key="index" class="show-todo">
            <todo-item :todoList="todoList" :todoItem="todoItem" :index="index"></todo-item>
        </div>
        <footer class="footer">
            <p>Double click to edit your todo</p>
            <p>Written by zxlg</p>
        </footer>
    </div>
</template>
<script>
    import todoItem from './todoItem.vue';

    export default {
        name: "todoList",
        components: {
            todoItem,
        },
        data() {
            return {
                todoInput: "",
                todoList: [],
            };
        },
        methods: {
            addTodoItem() {
                if (this.todoInput.trim()) {
                    this.todoList.push({
                        'text': this.todoInput,
                        'isCompleted': false
                    });
                };
                this.todoInput = "";
            },
        }
    };
</script>
<style lang="less">
.todo-list{
    width: 50%;
    min-width: 750px;
    margin: 0 auto;
    padding: 0 10px;

    .add-todo{
        display: flex;
        justify-content: flex-start;
        align-items: center;
        margin: 30px 0 ;
    }
    .form-control{
        width: 100%;
        min-width: 375px;
        height: 34px;
        padding: 6px 12px;
        font-size: 16px;
        line-height: 1.42857143;
        color: #555;
        background-color: #fff;
        background-image: none;
        border: 1px solid #ccc;
        border-radius: 4px;
        -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075);
        box-shadow: inset 0 1px 1px rgba(0,0,0,.075);
        -webkit-transition: border-color ease-in-out .15s,-webkit-box-shadow ease-in-out .15s;
        -o-transition: border-color ease-in-out .15s,box-shadow ease-in-out .15s;
        transition: border-color ease-in-out .15s,box-shadow ease-in-out .15s;

        margin-right:10px; 
    }
    .btn{
        display: inline-block;
        width: 88px;
        height: 48px;
        padding: 6px 12px;
        font-size: 16px;
        font-weight: 400;
        line-height: 1.42857143;
        text-align: center;
        white-space: nowrap;
        vertical-align: middle;
        -ms-touch-action: manipulation;
        touch-action: manipulation;
        cursor: pointer;
        -webkit-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        user-select: none;
        background-image: none;
        border: 1px solid transparent;
        border-radius: 4px;
        margin: 0 10px;
    }
    .btn-default{
        color: #333;
        background-color: #fff;
        border-color: #ccc;
    }
    .btn-default:hover {
        color: #333;
        background-color: #e6e6e6;
        border-color: #adadad;
    }
    .btn-success{
        color: #fff;
        background-color: #5cb85c;
        border-color: #4cae4c;
    }
    .btn-success:hover {
        color: #fff;
        background-color: #449d44;
        border-color: #398439;
    }
    .btn-danger{
        color: #fff;
        background-color: #d9534f;
        border-color: #d43f3a;
    }
    .btn-danger:hover {
        color: #fff;
        background-color: #c9302c;
        border-color: #ac2925;
    }

    .footer {
        color: #aaa;
        font-size: 12px;
        margin-top: 100px;
    }
}

</style>