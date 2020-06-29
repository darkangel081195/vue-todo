<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <h1>To Do App</h1>

    <Add @add-todo = "add" />

    <div class="container">
      <div class="pending">
        <h2>Pending</h2>
        <Todo :todoList = "pendingTodoList"
              @delete-todo = "deleteTodo"
        />
      </div>
      
      <div class="completed">
        <h2>Completed</h2>
        <Todo :todoList = "completedTodoList"
              @delete-todo = "deleteTodo"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Add from "./components/AddToDo";
import Todo from "./components/ToDo";

export default {
  name: 'App',
  components: {
    Add,
    Todo
  },

  data(){
    return{
      todoList : []
    }
  },
  methods:{

    //Adding new todo to the list
    add(event){
      this.todoList.push({id:Date.now(),task:event,done:false});
    },

    //Deleting todo from the list
    deleteTodo(id){
      this.todoList = this.todoList.filter(data => data.id !== id);
    }
  },
  computed:{

    //Separating todolist based on completion status
    pendingTodoList(){
      if(this.todoList.length === 0)return[]
      return this.todoList.filter(todo => !todo.done)
    },
    completedTodoList(){
      if(this.todoList.length===0)return[]
      return this.todoList.filter(todo => todo.done)
    }
  }
}
</script>

<style>
  @media (min-width: 700px) {
    .container{
      display : flex;
    }

    .pending{
      flex:1;
    }

    .completed{
      flex:1;
    }
  }
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 30px;
  }

  img{
    height:100px;
  }
</style>
