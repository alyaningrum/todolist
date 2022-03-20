<template>
  <div style="margin-top:25px">
    <ul class="list-group">
      <li v-for="(todo,index) in todos" :key="index" class="list-group-item">
        <div class="row">
          <div class="col">
            <span v-if="todo.isDelete">
              <del>
              {{ todo.activity }}
              </del>
            </span>
            <span v-else>
              {{ todo.activity }}
            </span>
          </div>
        <div class="col-auto">
          <div class="row gx">
            <div class="col">
              <button @click="deleteTodo(index)" class="btn btn-danger">Delete</button>
            </div>
          </div>
        </div>
      </div>
      </li>
      
    </ul>
  </div>
</template>

<script>
export default {
  props:{
    todos:{
      type:Array,
      default:[]
    }
  },
   setup(props,{emit}){
     const deleteTodo = index => {
       emit('deleteTodo',index)
     }

     return {deleteTodo}
  },
}
</script>