<template>
    <div class=container>
        <div id="task">

            <!-- Showing Task in form to enable easy edit access -->
            <form @submit.prevent="edit">
                <input 
                    type="text" 
                    :value="todo.task" 
                    ref="task" 
                    @blur="edit" 
                    :disabled="!isEdit"
                />
            </form>
        </div>

        <!-- Action buttons -->
        <div id="actions">
            <button 
                @click="todo.done = !todo.done" 
                id="done" 
                :class="{active:todo.done}"
                title = "Toggle Task Status"
            >
                <span class="fa fa-check"></span>
            </button>

            <button @click="toggle" id="edit" title="Edit Task">
                <span class="fa fa-edit"></span>
            </button>

            <button 
                @click="$emit('delete-todo',todo.id)" 
                id="delete" 
                title="Delete Task"
            >
                <span class="fa fa-trash"></span>
            </button>
        </div>
    </div>
</template>

<script>
export default {
    props:{
        todo:{
            type:Object,
            required:true
        }
    },
    data(){
        return{
            isEdit : false
        }
    },
    methods:{

        //Toggling status of the Edit button
        toggle(){
            this.isEdit = true;
            this.$nextTick(() => this.$refs.task.focus());
        },

        //Getting the new task value and emiting event to update the task
        edit(){
            const changedTask = this.$refs.task.value;
            if(!changedTask){
                alert("Task cannot be empty");
            }
            else{
                this.isEdit = false;
                this.$emit('edit-todo',changedTask);
            }
        }
    }

}
</script>

<style scoped>
    @media (min-width:500px){
        .container{
            width:500px;
            display : flex;
            display:flex;
            justify-content: flex-start;
            align-items: center;

        }
        #task{
            flex:1;
        }
    }
    .container{
        box-sizing: border-box;
        border:1px solid rgb(233, 230, 230);
        box-shadow: 0 2px 1px 1px #ccc;
        margin:2px auto;
        min-height:60px;
        padding:10px;
        width:80%;
    }

    #task input{
        padding:10px;
    }
    #task input[disabled]{
        background-color: white;
        border:none;
        font-size : 18px;
        font-weight:bold;
    }

    #actions button{
        border:1px solid #ccc;
        padding:7px;
        margin-right:10px;
        background-color:white;
        cursor: pointer;
        font-size : 16px;
    }
    #done{
        color:rgb(68, 224, 68);
    }
    #done:hover,
    #done.active{
        background-color:rgb(68, 224, 68);
        color:white;
    }
    .active{
        background-color:rgb(68, 224, 68);
        color:white;
    }
    #edit{
        color:rgb(78, 108, 241);
    }
    #edit:hover{
        background-color: rgb(142, 142, 240);
        color:white;
    }
    #delete{
        color:red;
    }
    #delete:hover{
        background-color: red;
        color:white;
    }
</style>