<template>
  <div>
    <!-- Sayı Arttırma Bölümü -->
    <h1 class="text-3xl font-bold text-center m-5">{{ number }}</h1>
    <p>This is the first Vue component in the project.</p>
    <button @click="increase" class="bg-blue-500 text-white px-4 py-2 rounded">Arttır</button>

    <hr />
    <!-- ... Diğer HR etiketleri ... -->

    <!-- Todo Uygulaması -->
    <div class="mx-auto w-full max-w-lg">
      <h1 class="text-3xl text-center my-5 font-bold text-green-600">First Todo App</h1>
      <div class="flex w-full gap-3">
        <input
          type="text"
          class="w-full bg-transparent border rounded-md p-2"
          placeholder="Add a new todo"
          v-model="newTodoItem.name"
        />
        <button class="px-3 py-1 bg-green-600 text-white font-bold rounded-md" @click="addNewTodo">
          Ekle
        </button>
      </div>
      <div class="mt-5">
        <ul class="space-y-3">
          <li
            class="border border-gray-700 rounded-md px-2 py-3 flex justify-between items-center"
            v-for="(item, index) in todos"
            :key="index"
          >
            <div class="flex items-center">
              <!-- Görev Adı veya Düzenleme Inputu -->
              <span
                v-if="!item.editMode"
                @click="toggleIsChecked(item)"
                :class="{ 'line-through text-gray-500': item.isChecked }"
              >
                {{ item.name }}
              </span>
              <input
                v-else
                type="text"
                class="border border-gray-700 bg-transparent rounded-sm"
                v-model="item.name"
              />
            </div>
            <div class="flex items-center justify-center gap-2">
              <button
                @click="editModeToggle(item)"
                class="px-3 py-1 bg-blue-600 text-white font-bold rounded-md"
              >
                {{ item.editMode ? 'Kaydet' : 'Düzenle' }}
              </button>
              <button
                @click="deleteTodo(index)"
                class="px-3 py-1 bg-red-600 text-white font-bold rounded-md"
              >
                Sil
              </button>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>
<script>
import { ref, reactive } from 'vue'

export default {
  setup() {
    const number = ref(0)
    console.log('number', number.value)

    const increase = () => {
      number.value += 1
    }

    // TODO-APP

    const newTodoItem = reactive({ name: '', isChecked: false })
    const todos = reactive([])

    const addNewTodo = () => {
      if (newTodoItem.name.trim() !== '') {
        todos.push({ ...newTodoItem, editMode: false })
        newTodoItem.name = ''
        newTodoItem.isChecked = false
      }

      console.log('todo', newTodoItem, todos)
    }

    const toggleIsChecked = (item) => {
      item.isChecked = !item.isChecked
    }

    const editModeToggle = (item) => {
      item.editMode = !item.editMode
    }

    const deleteTodo = (index) => {
      todos.splice(index, 1)
    }

    return {
      number,
      increase,
      newTodoItem,
      todos,
      addNewTodo,
      deleteTodo,
      toggleIsChecked,
      editModeToggle
    }
  }
}
</script>
