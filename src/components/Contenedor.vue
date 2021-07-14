<template>
    <div class="row">
        <div class="col s12 m7">
            <CardProyect v-for="(project, i) in projects" :data="project" :key="i"  />
        </div>
    </div>
</template>

<script>

    import CardProyect from './CardProyect';

export default {
    data:()=>({
        projects : [],
    }),
    components:{
        CardProyect,
    },
    mounted(){
        this.getProjects();
    },
    methods:{
        async getProjects(){

            const userId = JSON.parse(localStorage.getItem('user'));
            const idToken = userId.idToken;
            const localID = userId.localId;
            const resp = await fetch(`
                https://crud-vuejs-c6a95-default-rtdb.firebaseio.com/projects/${localID}.json?auth=${idToken}
            `)
            const data =  await resp.json()
            for(let i in data){
                this.projects.push({
                    id:i,
                    data:data[i]
                });
            }
            // console.log(this.projects)
        },
    }
}
</script>

<style scoped>

</style>