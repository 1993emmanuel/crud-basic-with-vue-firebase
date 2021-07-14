<template>
    <div id="navbar">
        <nav>
            <div class="nav-wrapper indigo lighten">
                <router-link to="/" class="brand-logo">Proyectos</router-link>
                <a href="#" data-target="mobile-demo" class="sidenav-trigger"><i class="material-icons">menu</i></a>
                <ul class="right hide-on-med-and-down">
                    <li>
                        <router-link to="/" v-if="!session">Registrar</router-link>
                    </li>
                    <li>
                        <router-link to="/login" v-if="!session">Login</router-link>
                    </li>
                    <li>
                        <router-link to="/proyectos" class="waves-effect indigo darken-3 btn" v-if="session">
                            Proyectos
                        </router-link>
                    </li>
                    <li>
                        <router-link to="/login" class="waves-effect  deep-orange btn" v-if="session" @click="cerrarSession">
                            Cerrar Session
                        </router-link>
                    </li>
                </ul>
            </div>
        </nav>

        <ul class="sidenav" id="mobile-demo">
            <li>
                <router-link to="/" v-if="!session">Registrar</router-link>
            </li>
            <li>
                <router-link to="/login" v-if="!session">Login</router-link>
            </li>
            <li>
                <router-link to="/proyectos" v-if="session">Proyectos</router-link>
            </li>
            <li>
                <router-link to="/login" class="waves-effect  deep-orange btn" v-if="session" @click="cerrarSession">
                    Cerrar Session
                </router-link>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    data:()=>({

    }),
    mounted(){
        M.AutoInit();

    },
    computed:{
        session(){
            const user = localStorage.getItem('user')
            if(user){
                return true;
            }
            return false
        }
    },
    methods:{
        cerrarSession(){
            localStorage.removeItem('user')
        }
    }
}
</script>

<style scoped>

</style>