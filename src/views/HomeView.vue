<script setup>
import { ref } from 'vue'
let isOpen = ref(false)

let api = 'https://jsonplaceholder.typicode.com/users/'
let arr = ref([])
let obj = ref({})
let title = ref('')
let body = ref('')
let idd = ref('')

function getAll() {
  fetch(api)
  .then(res => res.json())
  .then(data => arr.value = data )
}

function getUser(id) {
  fetch(api + id)
  .then(res => res.json())
  .then(data => obj.value = data )
}

function byId(event) {
  let userId = event.target.id;
  getUser(userId)
  setTimeout(() => {
    console.log(obj.value);
    
  }, 1000)
}

function post() {
  fetch(api, {
    method: 'POST',
    headers: {'Content-Type':'application/json'},
    body: JSON.stringify({
      title: title.value,
      body: body.value
    })
  }).then(res => res.json()).then(data => console.log(data))
}

function put() {
  fetch(api + idd.value, {
    method: 'PUT',
    headers: {'Content-Type':'application/json'},
    body: JSON.stringify({
      title: title.value,
      body: body.value
    })
  }).then(res => res.json()).then(data => console.log(data))
}

getAll()
</script>



<template>
  <section class="hero">
    <div class="container">
      <div class="hero__wrapper">
        <ul class="hero__list">
          <li class="hero__item" v-for="item in arr" :key="item.id" :id="item.id" @click="byId">
            {{ item.name }}
          </li>
        </ul>
        
        <div class="hero__card" :id="obj?.id">
          <h2 class="hero__title">{{ obj?.name }}</h2>
          <p class="hero__description">{{ obj?.username }}</p>
        </div>
        <button @click="isOpen = true">OPEN</button>
        <h2 v-if="isOpen" @click="isOpen = false">salom &copy;</h2>
      </div>
    </div>
  </section>

  <section class="post">
    <div class="container">
      <div class="post__wrapper">
        <input type="text" v-model="title">
        <input type="text" v-model="body">
        <button @click="post">POST</button>
        <input type="text" v-model="idd">
        <button @click="put">PUT</button>
      </div>
    </div>
  </section>
</template>
