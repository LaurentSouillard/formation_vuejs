<template>
  <Layout>
    <template v-slot:header>
      En-tête
    </template>
    <template v-slot:aside>
      Côté
    </template>
    <template v-slot:main>
      Principal
    </template>
    <template v-slot:footer>
      Pied de page
    </template>
  </Layout>
  <h1>TODO LIST</h1>
  <Button><strong>Demo</strong></Button>
  <form action="" @submit.prevent="addTodo">
    <fieldset role="group">
    <input type="text" placeholder="Tâche à effectuer" v-model="newTodo">
    <button>Ajouter</button>
  </fieldset>
  </form>
  <p v-if="todos.length == 0">La liste est vide</p>
  <div v-else>
  <ul>
    <li v-for="todo in todos">
      <!--<label for="">
        <input type="checkbox" v-model="todo.completed">
        {{ todo.title }}
      </label>-->
      <Checkbox :label="todo.title" class="class1" @check="" @uncheck=""/>
    </li>
  </ul>
</div>
<p v-if="remainingTodos > 0">

  {{ remainingTodos }} à faire

</p>
<Checkbox :label="'Bonjour'"/>
<hr>


  <h1>Bonjour {{ firstName.toUpperCase() }} compteur : {{ count }}</h1>
  <!-- pas de .value dans {{  }}-->
  <p>ça va ?</p>
  <button @click="count++">Increment</button>
  <button @click="decrement">Decrement</button>
  <!--<div v-show="count > 5">Bravo !</div>-->
  <div v-if="count < 5">Encore !</div>
  <div v-else-if="count > 5">Bravo !</div>
  <div v-else>Presque !</div>
  <ul>
    <li v-for="movie in movies" :key="movie">

      {{ movie }} <button @click="deleteMovie(movie)">supprimer</button>
    </li>
  </ul>
  <button @click="sortMovies">Sort</button>
  <form action="" @submit.prevent="addMovie">
    <input type="text" placeholder="New" v-model="movieName"> {{ movieName }}
    <button>add</button>
  </form>
  <hr>
  <ul>
    <li>{{ person.firstName }}</li>
    <li>{{ person.lastName }}</li>
    <li>{{ person.age }}</li>
    </ul>

    <button @click.prevent="randomAge">Changer âge</button>
</template>

<script setup>
import {computed, ref} from 'vue'
import Checkbox from './Checkbox.vue';
import Button from './Button.vue';
import Layout from './Layout.vue';

const remainingTodos = computed(() => {
  return todos.value.filter(t => t.completed == false).length
})

const todo = ref('')

const todos = ref([])

const newTodo = ref('')

const addTodo = () => {
  todos.value.push({
    title: newTodo.value,
    completed: false,
    date: Date.now()
})
newTodo.value = ''
}

const person = ref({
  firstName: 'John',
  lastName: 'Doe',
  age: 20
})

const randomAge = () => {
  person.value.age = Math.round(Math.random() * 100)
}

const count = ref(0)
const increment = () => {
  count.value++
};
const movies = ref([
  'Matix',
  'Lilo',
  'Titanic'
])
const decrement = () => {
  count.value--
};
const firstName = "John"
const movieName = ref('')
const deleteMovie = (movie) => {
  movies.value = movies.value.filter(m => m != movie)
}

const sortMovies = () => {
  movies.value.sort((a,b) => a > b ? 1 : -1)
}

const addMovie = () => {
  
  movies.value.push(movieName.value)
  movieName.value = ''
}

/*const addMovie = (event) => {
  event.preventDefault()
  movies.value.push(movieName.value)
  movieName.value = ''
}*/
</script>

<style>

h1{
  color: brown;
}

</style>