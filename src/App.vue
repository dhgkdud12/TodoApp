<template>
  <div id="app" class="container">
   <h1 class = "text-center">Todo App</h1>
   <input 
      v-model="todoText"
      type="text" 
      class="w-100 p-2" 
      placeholder="Type todo"
      @keyup.enter="addTodo"
      >
   <hr>
   <TodoList
    :todos ="todos" 
    @toggle-checkbox="toggleCheckbox"
    @click-delete="deleteTodo"
   /> 
   {{todos}}
  </div>
</template>

<script>
import TodoList from '@/components/TodoList';
export default {
  components:{
    TodoList
  },

  data(){
    return {
      todoText: '',
      todos:[
        {id: 1, text:'buy a car', checked: false},
        {id: 2, text:'play a game', checked: false},
      ]
    }
  },

  methods:{
    deleteTodo(id){
      // const index = this.todos.findIndex(todo => {
      //   return todo.id === id;
      // });
      // this.todos.splice(index, 1);
      this.todos = this.todos.filter(todo => todo.id !== id);
      //걸러서 넣어줌 
    },
    addTodo(e){
      this.todos.push({
        id:Math.random(),
        text: e.target.value,
        checked: false
      });
      this.todoText = '';
    },
    toggleCheckbox({id,checked}){ //구조 분해 할당
      const index = this.todos.findIndex(todo => {
        return todo.id === id;
      });
      this.todos[index].checked = checked;
    }
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
