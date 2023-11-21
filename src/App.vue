<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'

import { ref, onMounted, computed, watch } from 'vue'

const todos = ref([])
const name = ref('')

const input_content = ref('')


const todos_asc = computed(() => todos.value.sort((a, b) => {
  return a.createdAt - b.createdAt
}))


watch(name, (newVal) => {
  localStorage.setItem('name', newVal)
})


watch(todos, newVal => {
  localStorage.setItem('todos', JSON.stringify(newVal))
}, { deep: true })

const addList = () => {
  if (input_content.value.trim() === '' ) {
    return
  }

  todos.value.push({
    content: input_content.value,   
    done: false,
    editable: false,
    createdAt: new Date().getTime()
  })
}

const removeTodo = (todo) => {
	todos.value = todos.value.filter((t) => t !== todo)
}


onMounted(() => {
  name.value = localStorage.getItem('name') || ''
  todos.value = JSON.parse(localStorage.getItem('todos')) || []
})

</script>

<template>
  
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />
    <div class="wrapper">
      <HelloWorld msg="Vue Assignment" />
    </div>
  </header>

  <main class ="app">
  
    <h1 v-if="showWelcome">Welcome!</h1>
    <h1 v-else>Let's Go!</h1>
    <h2>{{ message }}</h2>
    Likes: <b> {{ count }}</b>
    <br>
    <div class = "clickButtons">
      <button @click="increateNumber" class="btn btn-primary">Like</button>
    </div>

    <br>

    <div class="rounded-md ...">
      <button @click="celebrateWelcome" class="btn btn-info">Let's go</button>
    </div>

    <hr>
    <div v-for="student in students"> 
      {{ student }}
    </div>
    <hr>
    <div v-for="m in ms"> 
      {{ m }}
    </div>
    <hr>

    <h2>{{ message }}</h2>
    Likes: <b> {{ count }}</b>
    <br>
    <button @click="decreaseNumber" class="btn btn-danger">Dislike</button>

    <hr>

    <section class="Listing">

        <h2>Listing</h2>

        <br>

        <form id="new-todo-form" @submit.prevent="addList">
          
          
          <div class="mt-10 grid grid-cols-1 gap-x-6 gap-y-8 sm:grid-cols-6">
            <div class="lg:col-span-4">
             
               <div class="mt-2">
                <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                  
                  <input type="text" name="content" id="content" placeholder="type in here....." v-model="input_content" />
          
                  <input type="submit" value="Add Name" />
                  <hr>
                   
                </div>
              </div>
            </div>
          </div>
        </form>
    </section>

    

    <section class="the lists">
      <h3>Lists</h3>
      <hr>
      <div class="list">
        <div v-for="todo in todos_asc" :class="`todo-item ${todo.done && 'done'}`">

        <br>
        <table class="table table-success table-striped">
        <tbody>
        <tr>
        
        <td>       
            <input type="text" v-model="todo.content" />        
        </td>

        <td>
            Likes: <b> {{ count }}</b>
            <button @click="likeNumber" class="btn btn-primary">Like</button>
        </td>

        <td>      
						<button class="btn btn-danger" @click="removeTodo(todo)">Delete</button>
        </td>
        
        </tr>
        </tbody>
        </table>

        </div>
      </div>
    </section>

    
    
    
  </main>
  
</template>

<script>

export default {
  data() {
    return {
      message: "Let's go.",
      count: 0,
      showWelcome: true,
      students: [
        'John',
        'Tom',
        'Jay'
      ],
      ms: [
        'RGM GM',
        'GP 01 FB',
        'RX 90'
      ]
    }
    
  },
  mounted() {
    console.log("Mounted");
    console.log("message >> "+ this.message);
    console.log('showWelcome',this.showWelcome);
    this.count = 0;
  },
  created() {
    console.log('created');
  },
  methods:{
    increateNumber() {
      console.log("Call increate Method");
      this.count += 1;
    },
    decreaseNumber() {
      console.log("Call increate Method");
      this.count -= 1;
    },
    likeNumber() {
      console.log("Call increate Method");
      this.count += 1;
    },
    celebrateWelcome() {
      this.showWelcome = false;
    },
    addList() {
      console.log("Adding List");
      return {
        names: [
          'Jake',
          'May',
          'James'
        ]
      }
    }
  }
}
</script>


<style scoped>
header {
  line-height: 2;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

.clickButtons {
  line-height: 1.5;
}


  
}
</style>
