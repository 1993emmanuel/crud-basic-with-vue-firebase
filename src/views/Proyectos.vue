<template>
  <div id="proyectos" class="container">
        <h1>Proyectos</h1>
        <div class="row">
            <router-link to="reg-projects"
                class="col s12 waves-effect green darken-4 btn">
                <i class="material-icons">add</i>
                Crear proyecto
            </router-link>
        </div>
        <Contenedor />
  </div>
</template>

<script>

// importamos el componente contenedor
import Contenedor from '../components/Contenedor';

export default {
    components:{
        Contenedor,
    }
}
</script>

<style>

</style>