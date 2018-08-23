<template>
    <div class="todo-item" :todoList="todoList" :todoItem="todoItem" :index="index">
        <div class="item-content">
            <div class="item-index" :class="{'grayIndex':todoItem.isCompleted}">{{index+1}}.</div>
            <label v-if="!edit" class="show-text"
            :class="{'todo-item-completed':todoItem.isCompleted}" 
            @dblclick="editTodoItem()"
            >{{todoItem.text}}
            </label>
            <input v-else type="text" class="input-edit-item"
            v-todo-item-focus="edit"
            v-model="todoItem.text"
            @blur="completeEdit(index)"
            @keypress.enter="completeEdit(index)" 
            >
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
        // 自定义指令
        directives: {
            'todo-item-focus': {
                // 指令的定义
                inserted: function (el) {
                    el.focus()
                }
            }
        },
        data() {
            return {
                edit: false,
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
                this.todoList.splice(this.index, 1);
            },
            editTodoItem() {
                this.edit = true;
            },
            completeEdit(index) {
                if (this.todoList[index].text.trim()) {
                    this.edit = false;
                } else {
                    this.todoList.splice(index, 1);
                }
            }
        }
    }
</script>

<style lang="less">
.todo-item{
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    align-items: center;
    margin: 10px 0;

    .item-content{
        width: 100%;
        min-width: 400px;
        height: 100%;
        display: flex;
        flex-direction: row;
        justify-content: flex-start;
        align-items: baseline;
        font-size: 16px;
        padding:5px 10px; 
        border-bottom: 1px solid #ddd;
        margin-right: 10px;

        .show-text{
            width: 100%;
            height: 100%;
            text-align: left;
            font-size: 16px;
            line-height: 1.42857143;
            margin: 6px 12px;
        }
    }
    .input-edit-item{
        width: 100%;
        padding: 5px 11px;
        font-size: 16px;
        line-height: 1.42857143;
        color: #555;
        background-color: #fff;
        background-image: none;
        border: 1px solid #ccc;
        border-radius: 4px;
        -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075);
        box-shadow: inset 0 1px 1px rgba(0,0,0,.075);
    }
    .item-index{
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
    color: #aaa;
}
.todo-item-completed{
    text-decoration: line-through;
    color: #aaa;
}
</style>
