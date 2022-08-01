<template>
  <div class="task">
    <div class="task__card" 
    v-for="(tarefa, index) in task" 
    :key="tarefa.name"
    @click="check(tarefa)"
    :class="!tarefa.pending ? 'done':''">
      <h3>{{tarefa.name}}</h3>
      <button @click="removerTarefa(index)" class="task__remove">X</button>
    </div>
  </div>
</template>

<script>
export default {
  props:{
    task: Array
  },
  methods:{
    removerTarefa(i){
      this.task.splice(i, 1)
    },
    check(el){
      el.pending = !el.pending
    }
  }
}
</script>

<style>
.task{
  display: grid;
  margin-top: 100px;
  grid-template-columns: repeat(4, 1fr);
  width: 100%;
  height: fit-content;
}

.task__card{
  display: flex;
  position: relative;
  margin: 20px;
  width: 250px;
  height: 100px;
  align-items: center;
  justify-content: center;
  border-radius: 10px;
  background-image: linear-gradient(-90deg, rgb(199, 45, 45) 95%, rgba(255, 0, 0, 0.548) 0%);
  color: white;
  cursor: pointer;
}

.task__remove{
  position: absolute;
  right: 5px;
  top: 5px;
  border: 0;
  color: white;
  border-radius: 50%;
  padding: 2px 5px;
  background-color: rgba(0, 0, 0, 0.432);
}

.done{
  background-image: linear-gradient(-90deg, rgb(45, 199, 65) 95%, rgba(9, 255, 0, 0.548) 0%);
  text-decoration: line-through;
}
</style>