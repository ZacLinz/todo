<template>
  <div class="container">
    <h1> Your To do List!</h1>
    <section class="input-panel">
      <md-field>
        <md-input v-model="currentTodo" @keyup.enter="addTodo()" placeholder="Add a todo"></md-input>
        </md-field>
    </section>
    <section class="list">
      <ul class="todo-list">
        <li v-for="todo in todos" :key="todo.id" :class="{completed: isChecked(todo)}">

            <input type="checkbox" class="checkbox" @click="check" v-model="todo.checked">

            <input type="text"
              v-if="todo === editingTodo"
              class="text-input"
              @blur="finishEdit(todo)"
              @keyup.enter="finishEdit(todo)"
              v-model="todo.label">

            <label class="todo-label" v-if="todo !== editingTodo" @dblclick="editTodo(todo)"> {{ todo.label }} </label>
            <span><md-button @click="removeTodo(todo)">X</md-button></span>

        </li>
      </ul>
    </section>
  </div>
</template>

<script>
export default {
  data(){
    return {
      todos: [],
      currentTodo: '',
      editingTodo: null
    };
  },
  methods: {
    addTodo(){
      this.todos.push({id: this.todos.length, label: this.currentTodo, completed: false});
      this.currentTodo = '';
    },

    removeTodo(todo){
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },

    editTodo(todo){
      this.editingTodo = todo;
    },

    finishEdit(todo){
      this.editingTodo = {};
      if (todo.label.trim() === ""){
        this.removeTodo(todo);
      }
    },

    check(todo){
      todo.checked = true;
    },

    isChecked(todo){
      return todo.checked;
    }

  }
};
</script>

<style>
body{
  background-color: #E83636;
  margin: 0 auto;
}

.container{
  width: 70%;
  margin: 5px;
}

.input-panel, li{
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: #FFFFFF;
  width: 100%;
  padding: 5px;
  list-style-type: none;
  border: 1px solid #CACACA;
}

.todo-label{
  padding-left: 10px;
}

.checkbox{
  padding: 15px;
}

li.completed{
  text-decoration: line-through;
}



.todo-list{
  background-color: #FFFFFF;
  width: 70%;
}

.todo-list li.editing .edit{
  display: block;
  padding: 10px;
}

.todo-list li.editing .view{
  display: none;
}
</style>
