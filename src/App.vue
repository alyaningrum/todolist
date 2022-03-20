<script>
import { reactive,ref,computed,onMounted,toRefs } from "vue";
import List from './components/list.vue'
export default {
components:{List},
  setup() {
    const todo = ref('')
    const todos = reactive({
      list: [],
    })

    onMounted(() => {
      const storage = JSON.parse(localStorage.getItem('todos'))
      if(storage)
        todos.list  = storage
    });

    const totalTodo = computed(() => {
      return todos.list.length
    }) 

    const progressBar = computed(() => {
       const bar = []
      todos.list.map(function(v){
      })
      
      return (bar.length / todos.list.length) * 100
    })

    const add = () => {
       todos.list.unshift({
         activity:todo.value,
         isDelete: false
       });

       todo.value = '';

       saveToStorage();
    }

    const deleteTodo = indexTodo => {
      todos.list = todos.list.filter((item,index) => {
        if (index != indexTodo) {
          return item
        }
      });

      saveToStorage();
    }

    const saveToStorage = () => {
      localStorage.setItem('todos',JSON.stringify(todos.list))
    }

    return {
      todo,
      ...toRefs(todos),
      totalTodo,
      progressBar,
      add,
      deleteTodo,
    }

  },
}

</script>

<template>
<div class="container" style="margin-top:80px"> 
    <div class="card-body col-6">
      <h2 class="card-title">My Todo list</h2>
      <div class="row">
        <div class="col-5">
        <br>
          <input type="text" v-model="todo" v-on:keyup.enter="add" class="form-control">
        </div>
        <div class="col">
          <br>
          <button class="btn btn-success" @click="add">Add</button>
        </div>
      </div>
      <list :todos="list" @deleteTodo="deleteTodo" />
      <br>
      </div>
    </div>
</template>


