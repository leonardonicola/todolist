<template>
<div class="todolist">
    <h1>Tarefas feitas</h1>
    <div class="todolist__progress">
        <div class="todolist__bar" ref="bar"><p>{{porcentagem}}%</p></div>
    </div>
    <input type="text" placeholder="Add a task!" 
    @keydown.enter="addTask">
    <Task :task="tarefa"/>
</div>
</template>

<script>
import Task from './Task.vue'
export default {
    components:{Task},
    data(){
        return{
            tarefa: [],
            porcentagem: 0
        }
    },
    methods:{
        addTask(el){
            const sameName = task => task.name === el.target.value
            const reallyNew = this.tarefa.filter(sameName).length == 0
            if(reallyNew && el.target.value != ''){
                this.tarefa.push({
                    name: el.target.value,
                    pending: true
                }) 
            }
            el.target.value = ''
        },
    },
    computed:{
        todolist(){
            return this.tarefa
        },
        feitas(){
            return this.tarefa.filter(elem => elem.pending == false)
        }
    },
    watch:{
        feitas(){
            localStorage.setItem('tarefa', JSON.stringify(this.tarefa))
            let lista = this.tarefa.length
            let done = this.feitas.length
            const bar = this.$refs.bar
            this.porcentagem = ((done/lista).toFixed(1))*100
            bar.style.width = `${this.porcentagem}%`
            if(lista <= 0){
                this.porcentagem = 0
                bar.style.width = "0%"
                bar.style.color = "#fff"
            }else if(this.porcentagem <= 45){
                bar.style.backgroundColor = "#A4161A"
                bar.style.color = "#fff"
            }else{
                bar.style.backgroundColor = "#04E762"
                bar.style.color = "#000"
            }
        }

    },
    created(){
        const json = localStorage.getItem('tarefa')
        this.tarefa = JSON.parse(json) || []
    }
}
</script>

<style>
.todolist{
    display: flex;
    flex-direction: column;
    justify-content: center;
    margin: 20px auto;
    text-align: center;
    color: #fff;
}

.todolist > h1{
    text-transform: uppercase;
}

.todolist__progress{
    position: relative;
    width: 70%;
    height: 30px;
    margin: 20px auto;
    border: 1px solid rgb(255, 255, 255);
    border-radius: 10px;
    overflow: hidden;
    background-color: rgba(0, 0, 0, 0.171);
}

.todolist__bar{
    width: 0%;
    height: 100%;
    background-color: rgba(255, 255, 255, 0.747);
}

.todolist__bar p{
    position: absolute;
    margin: 5px auto;
    left: 0;
    right: 0;
    
}

.todolist input{
    margin: 0 auto;
    width: 300px;
    height: 30px;
    border-radius: 10px;
    border: 2px solid rgb(0, 0, 0);
    padding: 20px;
}
</style>