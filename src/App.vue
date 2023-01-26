<script>

import axios from "axios";

export default {
  name: "App",

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
  <h1>TEST API</h1>
  <div v-for="project in projects" :key="project.id">
   <p>{{ project.name }}</p>
  </div>
</template>

<style>

</style>