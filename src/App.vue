<template>
  <div class="container">
    <h2>TODO LIST</h2>
    <form @submit.prevent="onAddTodo">
      <input type="text" v-model="todo" placeholder="Write a TODO" />
      <button type="submit">Add</button>
    </form>
    <small v-if="showError">Please Write a TODO and click the button</small>
    <div class="card">
      <div class="card-body" v-for="item in todos" :key="item.id">
        <div>
          <input type="checkbox" v-model="item.completed" />
          <span :class="{ 'todo-content': checked }">{{ item.content }}</span>
        </div>
        <button>wow</button>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  setup() {
    const todo = ref('')
    const todos = ref([])
    const showError = ref(false)
    const checked = ref(false)

    // 투두 추가
    const onAddTodo = () => {
      if (todo.value.length > 0) {
        // todos배열에 객체로 투두 push
        showError.value = false

        todos.value.push({
          id: Date.now(),
          content: todo.value,
          completed: false,
        })
        todo.value = ''
      } else {
        showError.value = true
      }
    }

    return {
      todo,
      todos,
      onAddTodo,
      showError,
      checked,
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

  small {
    color: red;
  }

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
    margin-bottom: 0.5rem;

    input {
      border: none;
      outline: none;
    }
    .todo-content {
      text-decoration: line-through;
      color: gray;
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
  .card {
    width: 70%;
    margin-top: 1rem;
  }
  .card-body {
    margin-bottom: 1rem;
    padding: 10px 30px;
    border-radius: 10px;
    border: 1px solid gray;
    background-color: rgba(244, 246, 246, 0.463);
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
}
</style>
