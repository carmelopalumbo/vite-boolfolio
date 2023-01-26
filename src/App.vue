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
      projects: []
    }
  },

  methods: {
    getApi(){
      axios.get(this.apiUrl)
      .then(result => {
        console.log(result.data);
        this.projects = result.data.projects;
      })
    }
  },

  mounted(){
    this.getApi();
  }
}
</script>

<template>
  <h1 class="text-center fw-bold py-4">TEST API</h1>
  <div class="container d-flex flex-wrap justify-content-between">
    <div v-for="project in projects" :key="project.id">
      <ProjectCard :project="project"/>
    </div>
  </div>
  
</template>

<style lang="scss">
@use "styles/app.scss";
</style>