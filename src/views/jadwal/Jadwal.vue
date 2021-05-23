<template>
  <div class="jadwal">
    <!--<img alt="Vue logo" src="../assets/logo.png"> -->
    <Slider />
    <hr class="my-3">
      <router-link class="btn btn-primary" to="/createjadwal">Add Jadwal</router-link>
    <table class="table table-striped">
  <thead>
    <tr>
        <th scope="col">ID</th>
      <th scope="col">Jadwal</th>
      <th scope="col">Nama Matakuliah</th>
      <th scope="col">Aksi</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(schedules, index) in schedules" :key="index">
      <td>{{ schedules.id }}</td>
      <td>{{ schedules.jadwal }}</td>
      <td>{{ schedules.matakuliah_id }}</td>
      <td>
        <router-link class="btn btn-success" :to="{name:'Editjadwal', params:{id:jadwals.id}}">Edit</router-link>
        <button @click.prevent="jadwalDelete(jadwals.id)" class="btn btn-danger">Delete</button>
      </td>
    </tr>
  </tbody>
</table>
  </div>
</template>

<script>
import axios from 'axios'
// @ is an alias to /src
// import Slider from "@/components/Slider.vue";
import { ref, onMounted } from 'vue';

export default {
  
  setup(){
    let schedules = ref([])

    onMounted(() => {
      axios.get('http://127.0.0.1:8000/api/schedules')
      .then(response => {
        schedules.value = response.data.data
      })
      .catch(error => {
        console.log(error)
      })
    })

    function jadwalDelete(id){
      axios.delete(`http://127.0.0.1:8000/api/schedules/${id}`)
      .then(()=>{
        let z = this.schedules.map(schedules => schedules.id).indexOf(id);
        this.schedules.splice(z, 1)
      }).catch(error => {
        console.log(error)
      })
    }

      return {
      schedules,
      jadwalDelete
    }
  }
};
</script>
