<template>
  <div class="home">
    <!--<img alt="Vue logo" src="../assets/logo.png"> -->
    <Slider />
    <hr class="my-3">
      <router-link class="btn btn-primary" to="/createmahasiswa">Add Mahasiswa</router-link>
    <table class="table">
  <thead>
    <tr>
      <th scope="col">Nama Mahasiswa</th>
      <th scope="col">Alamat</th>
      <th scope="col">No Telepon</th>
      <th scope="col">Email</th>
      <th scope="col">Aksi</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(mahasiswa, index) in students" :key="index">
      <td>{{ mahasiswa.nama_mahasiswa }}</td>
      <td>{{ mahasiswa.alamat }}</td>
      <td>{{ mahasiswa.no_tlp }}</td>
      <td>{{ mahasiswa.email }}</td>
      <td>
        <router-link class="btn btn-success" to="/editmahasiswa">Edit</router-link>
        <button class="btn btn-danger">Delete</button>
      </td>
    </tr>
  </tbody>
</table>
  </div>
</template>

<script>
import axios from 'axios'
// @ is an alias to /src
import Slider from "@/components/Slider.vue";
import { ref, onMounted } from 'vue';
export default {
  name: "Home",
  components: {
    Slider
  },
  setup(){
    let students = ref([])
    onMounted(() => {
      axios.get('http://127.0.0.1:8000/api/students')
      .then(response => {
        students.value = response.data.data
      })
      .catch(error => {
        console.log(error)
      })
    })
      return {
      students
    }
  }
};
</script>