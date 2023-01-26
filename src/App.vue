<script>

import axios from "axios";
import ProjectCard from "./components/ProjectCard.vue";

export default {
  name: "App",
  components: {
    ProjectCard
  },

  data(){
    return{
      apiUrl: 'http://127.0.0.1:8000/api/projects',
      projects: [],
      pagination: {
        currentPage: 1,
        lastPage: null
      }
    }
  },

  methods: {
    getApi(page){
      this.pagination.currentPage = page;
      axios.get(this.apiUrl, {
        params: {
          page: this.pagination.currentPage
        }
      })
      .then(result => {
        //console.log(result.data);
        this.projects = result.data.projects.data;
        this.pagination.currentPage = result.data.projects.current_page,
        this.pagination.lastPage = result.data.projects.last_page
      })
    }
  },

  mounted(){
    this.getApi(1);
  }
}
</script>

<template>
  <h1 class="text-center fw-bold py-4">TEST API</h1>
  <div class="container">
    <div class="row">
      <div class="col-4" v-for="project in projects" :key="project.id">
        <ProjectCard :project="project"/>
      </div>
    </div>
    <div class="d-flex justify-content-center py-4">
      <button :disabled="pagination.currentPage === 1" @click="getApi(1)" class="btn btn-dark me-2">FIRST</button>
      <button :disabled="pagination.currentPage === 1" @click="getApi(--pagination.currentPage)" class="btn btn-warning">PREVIOUS</button>
      <button :disabled="pagination.currentPage === item" @click="getApi(item)" class="mx-2 btn btn-info" v-for="item in pagination.lastPage" :key="item">{{ item }}</button>
      <button :disabled="pagination.currentPage === pagination.lastPage" @click="getApi(++pagination.currentPage)" class="btn btn-success">NEXT</button>
      <button :disabled="pagination.currentPage === pagination.lastPage" @click="getApi(pagination.lastPage)" class="btn btn-dark ms-2">LAST</button>
    </div>
  </div>
  
</template>

<style lang="scss">
@use "styles/app.scss";
</style>