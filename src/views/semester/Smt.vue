<template>
  <div class="semester">
    <!--<img alt="Vue logo" src="../assets/logo.png"> -->
    <Slider />
    <hr class="my-3">
      <router-link class="btn btn-primary" to="/createsmt">Add Semester</router-link>
    <table class="table table-striped">
  <thead>
    <tr>
      <th scope="col">ID</th>
      <th scope="col">Semester</th>
      <th scope="col">Aksi</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(data, index) in semesters" :key="index">
      <td>{{ data.id }}</td>
      <td>{{ data.semester }}</td>
      <td>
        <router-link class="btn btn-success" :to="{name:'Editsmt', params:{id:data.id}}">Edit</router-link>
        <button @click.prevent="smtDelete(data.id)" class="btn btn-danger">Delete</button>
      </td>
    </tr>
  </tbody>
</table>
  </div>
</template>

<script>
import axios from 'axios'
// @ is an alias to /src
import { ref, onMounted } from 'vue';

export default {
  
  setup(){
    let semesters = ref([])

    onMounted(() => {
      axios.get('http://127.0.0.1:8000/api/semesters')
      .then(response => {
        semesters.value = response.data.data
      })
      .catch(error => {
        console.log(error)
      })
    })

    function smtDelete(id){
      axios.delete(`http://127.0.0.1:8000/api/semesters/${id}`)
      .then(()=>{
        let z = this.semesters.map(semesters => semesters.id).indexOf(id);
        this.semesters.splice(z, 1)
      }).catch(error => {
        console.log(error)
      })
    }

      return {
      semesters,
      smtDelete
    }
  }
};
</script>
