<script setup>
  import { ref, computed } from 'vue';

  const favorites = ref([])
  const counter = ref(0);

  const cleanList = () => {
    favorites.value = [];
  }
  
  const increment = () =>{
    counter.value++;
  }

  const decrement = () => {
    counter.value--;
  };

  const resetCounter = () => {
    counter.value = 0
  }

  const addNumberSelected = (counter) => {
    favorites.value.push(counter);
  }

  const setColor = computed(() => {
    if(counter.value === 0 ){
      return 'reset'
    } else if (counter.value > 0) {
      return 'increment'
    } else{
      return 'dicrement'
    }
  })

  const swichButton = computed(()=>{
    const numSearch = favorites.value.find(num => num === counter.value);
    if (numSearch) {
      return true
    } else{
      return false
    }
  })

</script>

<template>
  <div class="container text-center">
    <div class="d-grid gap-2 d-md-flex justify-content-md-end">
    <button class="btn btn-primary me-md-2" @click="addNumberSelected(counter)" :disabled=swichButton type="button">Add Number</button>
    <button class="btn btn-danger me-md-2" @click="cleanList" type="button">Clean List</button>
    </div>
    <h1>Contardor: 
    <span :class=setColor> {{ counter }}</span>
    </h1>
    <div class="btn-group" role="group" aria-label="Basic mixed styles example">
      <button class="btn btn-danger" @click="decrement">-</button>
      <button class="btn btn-warning" @click="resetCounter">reset</button>
      <button class="btn btn-success" @click="increment">+</button>
      
    </div>

    <table  v-if="favorites.length > 0" class="table">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Numbers Selected</th>
        </tr>
      </thead>
      <tbody v-for="item , index in favorites" :key="index">
        <tr>
          <th scope="row">{{index}}</th>
          <td>{{item}}</td>
        </tr>
      </tbody>
    </table>

  </div>


  
</template>

<style scoped>

.container{
  border: solid;
  margin-top: 5px;
  padding: 10px;
}
.increment{
  color: green;
}

.dicrement{
  color: red;
}

.reset{
  color: black;
}

li{
  list-style: none;
}
</style>