<script>
export default {
    name: "ProjectCard",

    props:{
        project: Object
    }
}
</script>

<template>
  <div class="card my-3" style="width: 18rem;">
        <img src="..." class="card-img-top" alt="...">
            <div class="card-body">
                <h5 class="card-title">{{ project.name }}</h5>
                <p class="card-text">{{project.summary}}</p>
                <p class="text-center">TIPO: {{ project.type.name }}</p>
                <ul v-for="item in project.technologies" :key="item.id">
                    <li>{{ item.name }}</li>
                </ul>
            </div>
    </div>
</template>

<style>

</style>