<template>
    <div class="card horizontal" id="card-horizontal" v-if="data.data.status">
            <div class="card-stacked">
            <div class="card-content">
                <span class="card-title">{{data.data.title}}</span>
                <p>
                    {{data.data.description}}
                </p>
                <p>
                    Tecnologias : 
                    <span v-for="(lang,i) in data.data.langs" :key="i">
                        {{ i < data.data.langs.length-1 ? `${lang.toUpperCase()}, ` : lang.toUpperCase() }}
                    </span>
                </p>
            </div>
            <div class="card-action">
                <div class="row">
                    <router-link 
                        :to="`/edit-project/${data.id}`" 
                        class="col s6 waves-effect orange lighten-2 btn">
                        <i class="material-icons">edit</i>
                    </router-link>
                    
                    <button 
                        @click="deleteProject"
                        href="" class="col s6 waves-effect red lighten-1 btn">
                        <i class="material-icons">delete</i>
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {

    props:{
        data : Object,
    },
    computed:{
    },
    methods:{
        async deleteProject(){
            const userId = JSON.parse(localStorage.getItem('user'));
            const idToken = userId.idToken;
            const localID = userId.localId;

            const idProjectDelete = this.data.id
            const respuesta = await fetch(`
                https://crud-vuejs-c6a95-default-rtdb.firebaseio.com/projects/${localID}/${idProjectDelete}.json?auth=${idToken}`,
                {
                    method : 'PATCH',
                    body : JSON.stringify({status : false})
                }
            )
            const data = await respuesta.json()
            this.data.data.status = data["status"];
            // console.log(data)

        }
    }

}
</script>

<style scoped>

</style>