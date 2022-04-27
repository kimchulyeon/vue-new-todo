<template>
  <div class="container">
    <h2>TODO LIST</h2>
    <form @submit.prevent="onAddTodo">
      <input type="text" v-model="todo" placeholder="Write a TODO" />
      <button type="submit">Add</button>
    </form>
    <ul>
      <li v-for="(item, idx) in todos" :key="idx">
        {{ item.content }}
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  setup() {
    const todo = ref('')
    const todos = ref([])

    // 투두 추가
    const onAddTodo = () => {
      if (todo.value.length > 0) {
        // todos배열에 객체로 투두 push
        todos.value.push({
          id: Date.now(),
          content: todo.value,
        })
        todo.value = ''
      }
    }

    return {
      todo,
      todos,
      onAddTodo,
    }
  },
}
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  padding: 2rem;
  margin: 2rem auto 0;
  width: 80%;

  h2 {
    font-weight: bold;
    font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
    font-size: 2rem;
    color: rgb(0, 102, 255);
    margin: 0;
    margin-bottom: 2rem;
  }

  form {
    padding: 10px 1rem;
    border-radius: 10px;
    box-shadow: 0px 0px 12px rgba(0, 0, 0, 0.2);

    input {
      border: none;
      outline: none;
    }
    button {
      background-color: rgba(33, 121, 244, 0.828);
      color: white;
      border: none;
      padding: 5px 10px;
      border-radius: 5px;
      cursor: pointer;
    }
  }
}
</style>
