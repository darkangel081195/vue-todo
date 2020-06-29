<template>
    <div>
        <form @submit.prevent="add">
            <input type="text" placeholder=" Add Task " v-model="task"/>
        </form>
    </div>
</template>

<script>
export default {
    data(){
        return{
            task : ""
        }
    },
    methods:{
        add(){
            this.$emit("add-todo",this.task);
            this.task = "";
        }
    }
}
</script>

<style scoped>
    input{
        margin:10px auto;
        width:400px;
        height : 3em;
        border:1px solid rgb(211, 208, 208);
        border-radius:0.25rem;
        padding:10px;
        box-sizing: border-box;
    }

    input:focus{
        color: #495057;
        background-color: #fff;
        border-color: #41b883;
        outline: 0;
        box-shadow: 0 0 0 0.2rem rgba(65,184,131,.25)
    }

</style>