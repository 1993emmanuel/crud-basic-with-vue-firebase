<template>
    
    <div class="container" id="editProject">
        <div class="row">
            <router-link to="/proyectos"
                class="col s12 waves-effect blue lighten-2 btn">
                <i class="material-icons">arrow_back</i>
                regresar
            </router-link>
        </div>
        <div class="row">
            <form  @submit.prevent="editProject" class="col s12">
                <div class="row">
                    <div class="input-field col s12">
                        <input 
                            id="first_name"
                            type="text"
                            class="validate"
                            v-model.trim="project.title"
                            placeholder="titulo del proyecto">
                        <label for="first_name"></label>
                    </div>
                    <div class="input-field col s12">
                        <input 
                            id="last_name"
                            type="text"
                            class="validate"
                            v-model.trim="project.description"
                            placeholder="descripcion del proyecto">
                        <label for="last_name"></label>
                    </div>

                    <p>
                        <label>
                            <input type="checkbox" checked="checked" v-model="project.langs" value="html" />
                            <span>HTML</span>
                        </label>
                    </p>

                    <p>
                        <label>
                            <input type="checkbox" checked="checked" v-model="project.langs" value="css" />
                            <span>CSS</span>
                        </label>
                    </p>

                    <p>
                        <label>
                            <input type="checkbox" checked="checked" v-model="project.langs" value="js" />
                            <span>JS</span>
                        </label>
                    </p>

                    <p>
                        <label>
                            <input type="checkbox" checked="checked" v-model="project.langs" value="python" />
                            <span>PYTHON</span>
                        </label>
                    </p>

                    <p>
                        <label>
                            <input type="checkbox" checked="checked" v-model="project.langs" value="vue" />
                            <span>VUE</span>
                        </label>
                    </p>

                    <div class="row">
                        <button class="col s12 btn waves-effect waves-light" type="submit" name="action">Submit
                            <i class="material-icons right">send</i>
                        </button>
                    </div>
                </div>
            </form>
        </div>
    </div>


</template>

<script>

    import router  from '../router/index';

export default {

    data(){
        return{
            project : {},
            urlId : this.$route.params.id,
        }
    },
    mounted(){
        this.getProject();
    },
    methods:{
        async getProject(){

            const userId = JSON.parse(localStorage.getItem('user'));
            const idToken = userId.idToken;
            const localID = userId.localId;

            const resp = await fetch(`
                https://crud-vuejs-c6a95-default-rtdb.firebaseio.com/projects/${localID}/${this.urlId}.json?auth=${idToken}`
            );
            const data = await resp.json();
            this.project = data;
            // console.log(data)
        },
        async editProject(){
            const userId = JSON.parse(localStorage.getItem('user'));
            const idToken = userId.idToken;
            const localID = userId.localId;

            await fetch(`
                https://crud-vuejs-c6a95-default-rtdb.firebaseio.com/projects/${localID}/${this.urlId}.json?auth=${idToken}`,{
                    method : 'PATCH',
                    body : JSON.stringify(this.project)
                }
            );
            router.push('/proyectos');
        }
    }

}
</script>

<style scoped>

</style>