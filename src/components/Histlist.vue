<template>
<form>
    <!-- <label>Search By Code...</label> -->
    <input type="text" v-model="search" placeholder="Search By Code (e.g: H 3/86)">
    </form>
    <div class="tbl-header">
    <table cellpadding="0" cellspacing="0" border="0">
      <thead>
        <tr>
          <th>Code</th>
          <th>Age</th>
          <th>Sex</th>
          <th>BodyWeight</th>
          <th>BrainWeight</th>
        </tr>
      </thead>
    </table>
  </div>

   <div class="tbl-content">
    <table cellpadding="0" cellspacing="0" border="0">
      <!-- <tbody> -->
        <tbody v-for="user in matchingCodes" :key="user._id">
            <tr>
                    <router-link :to="{ name: 'Details', params: {id: user._id} }" target="_blank" class="router-link">
                        <td>{{ user.Code }}</td>
                    </router-link>
                    <td>{{ user.Age }}</td>
                    <td>{{ user.Sex }}</td>
                    <td>{{ user.BodyWeight }}</td>
                    <td>{{ user.BrainWeight }}</td>
            </tr>
        </tbody>
        <tbody v-if="!isPresent">
          <tr><td>No such record found!</td></tr>
        </tbody>
      <!-- </tbody> -->
    </table>
  </div>
<Footer />

</template>

<script>
import Footer from './Footer'
import SingleHist from './SingleHist'
import { ref, computed } from 'vue'
export default {
    props:['users'],
    components: { SingleHist, Footer },
    setup(props){

        const search = ref('')
        // const temp_users = ref(null)

        const temp_users = props.users

        const matchingCodes = computed(() => {
            return props.users.filter((user) => user.Code.includes(search.value))
        })

        const isPresent = computed(() => {
            search.value = search.value.toUpperCase()
            if(temp_users.find(user => user.Code.includes(search.value))){
                return true
            } else {
                return false
            }
        })

        return {matchingCodes, search, temp_users, isPresent}
    }
}
</script>

<style>

    form {
    max-width: 100vh;
    margin: 15px auto;
    background: rgba(255,255,255);
    text-align: left;
    padding: 15px 20px;
    border-radius: 10px;
  }

  input {
    font-size: 15px;
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: rgb(71, 71, 71);
  }
  input:focus{
      outline: none;
  }

    table{
    width:100%;
    table-layout: fixed;
    }
    .tbl-header{
    background-color: rgba(255,255,255,0.3);
    }
    .tbl-content{
    overflow-x:auto;
    margin-top: 0px;
    border: 1px solid rgba(255,255,255,0.3);
    }
    th{
    padding: 20px 15px;
    text-align: center;
    font-weight: 600;
    font-size: 20px;
    /* color: rgb(20, 84, 145); */
    color: rgb(206, 250, 185);

    text-transform: uppercase;
    }
    td{
    padding: 15px;
    text-align: center;
    vertical-align:middle;
    font-weight: 300;
    font-size: 18px;
    color: #fff;
    border-bottom: solid 1px rgba(255,255,255,0.1);
    }
    .router-link{
        text-decoration: underline;
        text-decoration-color: white;
    }

    /* demo styles */

    @import url(https://fonts.googleapis.com/css?family=Roboto:400,500,300,700);
    body{
    /* background: -webkit-linear-gradient(left, #25c481, #25b7c4);
    background: linear-gradient(to right, #25c481, #25b7c4);
     */
     background: linear-gradient(to right, #667db6, #0082c8, #0082c8, #667db6);
    font-family: 'Roboto', sans-serif;
    }
    section{
    margin: 50px;
    }


    /* for custom scrollbar for webkit browser*/

    ::-webkit-scrollbar {
        width: 6px;
    } 
    ::-webkit-scrollbar-track {
        -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3); 
    } 
    ::-webkit-scrollbar-thumb {
        -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3); 
    }

    

</style>