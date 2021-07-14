<template>
    <div class="container" id="created">
        <div class="row">
            <router-link to="proyectos"
                class="col s12 waves-effect blue lighten-2 btn">
                <i class="material-icons">arrow_back</i>
                regresar
            </router-link>
        </div>
        <div class="row">
            <form  @submit.prevent="createProject" class="col s12">
                <div class="row">
                    <div class="input-field col s12">
                        <input id="first_name" type="text" class="validate" v-model.trim="project.title">
                        <label for="first_name">Nombre del proyecto</label>
                    </div>
                    <div class="input-field col s12">
                        <input id="last_name" type="text" class="validate" v-model.trim="project.description">
                        <label for="last_name">Descripcion del proyecto</label>
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

    // agregamos router para poder redirigir a las rutas que necesitemos y con el push simplemente pasamos la ruta
    import router from '../router/index';

export default {
    data(){
        return{
            project : {
                title : "",
                description : "",
                langs : [],
                status : true
            },
        }
    },
    methods:{
        async createProject(){
            const userId = JSON.parse(localStorage.getItem('user'));
            const idToken = userId.idToken;
            const localID = userId.localId;
            await fetch(`
                https://crud-vuejs-c6a95-default-rtdb.firebaseio.com/projects/${localID}.json?auth=${idToken}`,
                {
                    method: "POST",
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