<!-- src/components/ItemList.vue -->
<script setup lang="ts">
import { ref } from 'vue'

interface Item {
  name: string
  price: number
}

const items = ref<Item[]>([
  { name: '東京科学大学', price: 100000000000 },
  { name: 'りんご', price: 160 }
])


const newItemName = ref('') 
const newItemPrice = ref(0) 

const addItem = () => { 
   if (items.value.some((item) => item.name === newItemName.value)) return
  items.value.push({ name: newItemName.value, price: newItemPrice.value }) 
} 

const deleteItem = (name: string) => { 
  items.value = items.value.filter((item) => item.name !== name) 
} 

interface Todo {
  name: string
}

const todos = ref<Todo[]>([
  { name: 'これを完成させる' },{ name: 'atcoderのレートを2年生までに1000以上にする' },
])
const donetodos = ref<Todo[]>([])

const newTodoName = ref('')

const addTodo = () => { 
   if (todos.value.some((todo) => todo.name === newTodoName.value)) return
  todos.value.push({ name: newTodoName.value }) 
} 
const completeTodo = (name: string) =>{
  const tododone = todos.value.find((tododone) => tododone.name == name)
  if (tododone) donetodos.value.push(tododone)
  todos.value = todos.value.filter((tododone) => tododone.name !== name)
}

const deleteTodo = (name: string) => { 
  todos.value = todos.value.filter((todo) => todo.name !== name) 
} 
const deletedoneTodo = (name: string) => { 
  donetodos.value = donetodos.value.filter((todo) => todo.name !== name) 
} 
</script>

<template>
  <div>
    <div>ItemList</div>
    <ul>
       <li v-for="item in items" :key="item.name" :class="{ over500: item.price >= 500 }">
        <div>名前: {{ item.name }}</div>
        <div>{{ item.price }} 円</div>
        <div v-if="item.price >= 10000">高額商品</div>
        <button @click="deleteItem(item.name)">削除</button>
      </li>
    </ul>
    <div>
      <label>
        名前
        <input v-model="newItemName" type="text" />
      </label>
      <label>
        価格
        <input v-model="newItemPrice" type="number" />
      </label>
      <button @click="addItem">追加</button>
    </div>
  </div>
  <div>
    <div>Todoリスト</div>
    <ul>
       <li v-for="todo in todos" :key="todo.name">
        <div>やること: {{ todo.name }}</div>
        <button @click="deleteTodo(todo.name)">削除</button>
        <button @click="completeTodo(todo.name)">完了にする</button>
      </li>
    </ul>
    <div>
      <label>
       名前 
        <input v-model="newTodoName" type="text" />
      </label>
      <button @click="addTodo">追加</button>
    </div>
    <div>
      <div>完了済み</div>
      <ul>
        <li v-for="donetodo in donetodos" :key="donetodo.name">
          <div>完了：{{ donetodo.name }}</div>
          <button @click="deletedoneTodo(donetodo.name)">削除</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<style>
.over500 { 
  color: red; 
} </style>