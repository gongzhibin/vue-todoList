<template>
    <div class="todo-item" :todoList="todoList" :todoItem="todoItem" :index="index">
        <div class="item-content">
            <div class="item-index" :class="{'grayIndex':todoItem.isCompleted}">{{index+1}}.</div>
            <label
            :class="{'todo-item-completed'
            :todoItem.isCompleted}" 
            :disabled="isDisabled" 
            @dblclick="editTodoItem"
            >{{todoItem.text}}
            </label>
        </div>

        
        <div class="btn-list">
            <button class="btn" 
            :class="{'btn-success'
            :!todoItem.isCompleted,'btn-default':todoItem.isCompleted}" 
            @click="changeComplete">{{isDone}}</button>

            <button class="btn btn-danger" 
            @click="deleteTodoItem">delete</button>
        </div>

    </div>
</template>
<script>
    export default {
        name: "todoItem",
        props: {
            todoList: {
                type: Array,
                default: [],
                required: true
            },
            todoItem: {
                type: Object,
                default: {},
                required: true
            },
            index: {
                type: Number,
                default: -1,
                required: true
            }
        },
        data() {
            return {
                isDisabled: true
            }
        },
        computed: {
            isDone() {
                return this.todoItem.isCompleted ? 'unDone' : 'done'
            }
        },
        methods: {
            changeComplete() {
                this.todoItem.isCompleted = !this.todoItem.isCompleted;
            },
            deleteTodoItem() {
                console.log(this.index);
                this.todoList.splice(this.index, 1);
            },
            editTodoItem() {
                console.log('dbc');
                this.isDisabled = false;
            }
        }
    }
</script>

<style lang="less">
.todo-item{
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    align-items: baseline;

    margin: 10px 0;

    .item-content{
        width: 100%;
        min-width: 400px;
        display: flex;
        flex-direction: row;
        justify-content: flex-start;
        align-items: baseline;
        font-size: 16px;
        padding:10px; 
        border:none;
        margin-right: 10px;
    }
    .item-content:disabled{
        background-color: #fff;
        cursor: default;
    }
    .btn-list{
        display: flex;
        flex-direction: row;
        justify-content: flex-end;
        align-items: baseline;
    }
}
.grayIndex{
    color: #888;
}
.todo-item-completed{
    text-decoration: line-through;
    color: #888;
}
</style>
