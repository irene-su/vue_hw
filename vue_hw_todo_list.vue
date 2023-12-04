<script setup>
import { ref} from 'vue'

let id = 0
const title = "Todo list"
const newTodo = ref('')

const todos = ref([])


function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}
function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>

<template>
  <h1 class="title">{{ title }}</h1>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo" placeholder="Do something...">
    <button>新增</button>
  </form>
  <ol>
    <li v-for="todo in todos" :key="todo.id"  class="todo-item">
      <input type="checkbox" v-model="todo.done" >
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
<!--       <button @click="removeTodo(todo)">X</button> -->
			<button class="remove-button" @click="removeTodo(todo)">X</button>
    </li>
  </ol>
<!--   <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? 'Show all' : 'Hide completed' }}
  </button> -->
</template>

<style>
.todo-item {
  border-bottom: 1px solid #ccc; /* 添加底边框作为分隔线 */
  padding-bottom: 5px; /* 可以根据需要调整底部内边距 */
  margin-bottom: 5px; /* 可以根据需要调整底部外边距 */
}
.remove-button {
	float: right; /*将按钮浮动到右侧
  margin-left: auto
/*   margin-left: auto */
/*   margin-left: auto */
/*   vertical-align: ; /* 调整垂直对齐方式 */
/*   margin-left: 100px; 可以根据需要调整左边距 */ 
}
.done {
  text-decoration: line-through;
}
  

</style>