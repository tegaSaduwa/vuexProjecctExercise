<template>
<div>
  <h3>Todos</h3>
  <div class="legend">
    <span>Double-click to mark as complete</span>
    <span>
      <span class="complete">complete</span>
    </span>
    <span>
      <span class="incomplete">incomplete</span>
    </span>
  </div>
  <div v-for="todo in allTodos" 
  :key="todo.id" 
  class="todo"
  v-bind:class="{'is-completed': todo.completed}"
  @dblclick="dblclick(todo)"> 
  {{ todo.title }} 
     <span @click="deleteTodo(todo.id)">x</span></div>
  </div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex';

export default {
  name: "Todos",
  methods: {
    ...mapActions(['fetchTodos','deleteTodo','updateTodo']),
    dblclick(todo) {
      const updTodo = {
        id: todo,
        title: todo.title,
        completed: !todo.completed
      }
      this.updateTodo(updTodo);
    }
  },
  computed: mapGetters(['allTodos']),
  created () {
    this.fetchTodos();
  }
};
</script>

<style scoped>
span {
  position: absolute;
  bottom: 10px;
  right: 10px;color: #fff;
  cursor: pointer;
}
.todos {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap:1rem;
}
.todo {
  border: 1px solid #ccc;
  background: #41b883;
  padding: 1rem;
  border-radius:5px;
  text-align: center;
  position: relative;
  cursor: pointer;
}
.legend {
  display: flex;
  justify-content: space-around;
  margin-bottom: 1rem;
}

.complete {
  display:inline-block;
  width:10px;
  height:10px;
  background: #35495e;
}

.incomplete {
  display:inline-block;
  width:10px;
  height:10px;
  background: #41b883; 
}

.is-complete {
  background: #35495e;
  color: #fff;
}

@media (max-width: 500px) {
  .todos{
    grid-template-columns: 1fr;
  }
}
</style>
