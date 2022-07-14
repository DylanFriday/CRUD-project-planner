<template>
<div class="project" :class="{complete:project.complete}">
    <div class="flexing">
        <div>
         <h3  @click="opendetail = !opendetail">{{project.title}}</h3>
         </div>
         <div>
             <span class="material-symbols-outlined" @click="deleteProject">
    delete
    </span>
    <router-link :to="{name: 'EditProject',params:{id:project.id} }">
<span class="material-symbols-outlined">
    edit
    </span>
    </router-link>

    
    <span class="material-symbols-outlined" @click="completeProject">
    done
    </span>
         </div>
    </div>

    <div v-if="opendetail">
        <p style="color: green">{{project.detail}}</p>
    </div>
   
  </div>

</template>

<script>
export default {
    props:['project'],
    data(){
        return{
            opendetail: false,
            api: 'http://localhost:3000/projects/'
        }
    },
    methods:{
        deleteProject(){
            let deleteRoute = this.api+this.project.id
            fetch(deleteRoute,{method:"DELETE"})
            .then(()=>{
                this.$emit("delete",this.project.id)
            })
            .catch((err)=>{
                console.log("err")
            })
        },
        completeProject(){
            let updateCompleteRoute = this.api + this.project.id
            fetch(updateCompleteRoute,{
                method:"PATCH",
                headers:{
                    "Content-Type": "application/json"
                },
                body: JSON.stringify(
                    {
                        complete: !this.project.complete
                    }
                )
                })
                .then(()=>{
                    this.$emit("complete",this.project.id)
                })
                .catch((err)=>{
                    console.log(err)
                })
        }
    }
}
</script>

<style>
.project{
    padding: 20px;
    background-color: #f2f2f2;
   border-left: 8px solid rgb(211, 117, 117);
   border-radius: 10px;
    margin: 10px;

}
h3{
    color: rgb(241, 146, 178);
     cursor: pointer;
}
.flexing{
    display: flex;
    justify-content: space-between;
    align-items: center;
}
span{
    margin-left: 10px;
}
span:hover{
    color: #777;
     cursor: pointer;
}
.complete{
    border-left-color: rgb(118, 228, 118);
}
</style>