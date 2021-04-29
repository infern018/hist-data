<template>
  <div class="home">
    <h1>Brain Histology Data Collection</h1>
    <Histlist :users="users" />
  </div>
</template>

<script>
import Histlist from '../components/Histlist.vue'
import { ref } from 'vue'

export default {
  name: 'Home',
  components: { Histlist },
  mounted(){
    console.log("konichiwa!")
  },
  setup(){

    // const search = ref('')
    const users = ref([])

    fetch('https://histdataapi.herokuapp.com/posts')
    .then(res => res.json())
    .then(data => {
        users.value = data
        console.log(users.value[0].Code)
    })

    return {users}

  }
}
</script>

<style>
  h1{
  font-size: 35px;
  color: #fcf6f5ff;
  text-transform: uppercase;
  font-weight: 600;
  text-align: center;
  margin-bottom: 15px;
}

  @media only screen and (max-width: 480px) {
    h1{
      font-size: 25px;
    }
  }

</style>
