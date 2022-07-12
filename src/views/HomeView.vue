<template>
  <div class="home">
    <h1>Home</h1>
    <div v-for="project in projects" :key="project.id">
   <Singleproject :project="project" @delete="deleteProject" @complete="completeProject"></Singleproject>
    </div>
  </div>
</template>

<script>
import Singleproject from '../components/Singleproject'
// @ is an alias to /src


export default {
  name: 'HomeView',
  components: {
    Singleproject,
   
  },
  data(){
    return{
      projects:[]
    }
  },
  methods:{
    deleteProject(id){
      this.projects = this.projects.filter(project=>{
        return project.id !=id;
      })
    },
    completeProject(id){
      let findProject = this.projects.find(project=>{
        return project.id === id;
      });
      findProject.complete = !findProject.complete
    }
  },
  mounted(){
    fetch(' http://localhost:3000/projects')
    .then((response)=>{
      return response.json()
    })
    .then((datas)=>{
      this.projects = datas
    })
    .catch(()=>{
      
    })
  }
}
</script>
