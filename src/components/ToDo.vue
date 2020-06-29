<template>
    <div>
        <button 
            :disabled="sortedTodoList.length===0" 
            :class="{active:isSort}"
            @click="isSort = !isSort"
        >
            Sort <span class="fa fa-sort-alpha-asc"></span>
        </button>
        <div v-for="todo in sortedTodoList" :key="todo.id">
            <TodoItems :todo = "todo" 
                       @delete-todo = "deleteTodo"
                       @edit-todo = "editTodo(todo,$event)"/>
        </div>
    </div>
</template>

<script>

import TodoItems from "./TodoItems";

export default {
    components:{TodoItems},
    props:{
        todoList:{
            type:Array,
            required:true
        }
    },
    data(){
        return{
            isSort : false,
        }
    },
    methods:{

        //Emit event to parent to delete the todo from list
        deleteTodo(id){
            this.$emit('delete-todo',id);
        },

        //Changing the description of the todo
        editTodo(todo,changedTask){
            todo.task = changedTask;
        }
    },
    computed:{

        //Sorting the todolist if sorting is selected
        sortedTodoList(){
            console.log("Inside sorted",this.isSort);
            if(this.isSort){
                return this.todoList.slice(0).sort((a,b)=>{
                    if (a.task < b.task)
                        return -1;
                    if (a.task > b.task)
                        return 1;
                    return 0;
                });
            }
            else{
                return this.todoList;
            }
        }
    }
}
</script>

<style scoped>
    button{
        color : #409EFF;
        background : none;
        border: 1px solid #ccc;
        padding:10px;
        border-radius : 3px;
        cursor:pointer;
    }
    button:hover,.active{
        color : white;
        background:#409EFF;
        outline : 0;
    }
    button[disabled]{
        color:grey;
        cursor:not-allowed;
    }

</style>

