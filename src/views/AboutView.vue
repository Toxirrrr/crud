<script setup>
let api = 'https://jsonplaceholder.typicode.com/users/'
function getAll() {
  fetch(api)
  .then(res => res.json())
  .then(data => console.log(data))
}
getAll()
</script>



<template>
  <section class="hero">
    <div class="container">
      <div class="hero__wrapper">
        <h2 class="hero__header">
        </h2>        
      </div>
    </div>
  </section>
</template>
