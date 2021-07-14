<template>
    <div id="register" class="container">
        <div class="row">
            <h1>Register</h1>
            <hr>
            <form class="col s12" @submit.prevent="validarPassword" >
                <div class="row">
                    <div class="input-field col s12">
                        <input id="email" type="email" class="validate" v-model.trim="email">
                        <label for="email">Email</label>
                    </div>
                </div>
                <div class="row">
                    <div class="input-field col s12">
                        <input id="password1" type="password" class="validate" v-model.trim="pass1">
                        <label for="password">Password</label>
                    </div>
                </div>
                <div class="row">
                    <div class="input-field col s12">
                        <input id="password2" type="password" class="validate" v-model.trim="pass2">
                        <label for="password">Confir Password</label>
                    </div>
                </div>
                <div class="row">
                    <button class="waves-effect waves-light btn-large" type="submit">Registrar</button>
                </div>
            </form>
        </div>
    </div>
</template>

<script>

    import router from '../router/index';

export default {
    data:()=>({
        email : "",
        pass1 : "",
        pass2 : "",
    }),
    methods:{
        async validarPassword(){
            if(this.pass1 === this.pass2 && this.pass1.length >= 6 && this.email!="" ){
                const API_KEY = "AIzaSyCSZKbeseFkGDvL1b6hpsB6Jim726wM_oI";
                // registrar al usuario
                const respuesta = await fetch(`https://identitytoolkit.googleapis.com/v1/accounts:signUp?key=${API_KEY}`,{
                    method:'POST',
                    body : JSON.stringify({
                        email : this.email,
                        password : this.pass1,
                        returnSecureToken : true
                    })
                });
                const data = await respuesta.json();
                localStorage.setItem('user',JSON.stringify(data));
                router.push('/proyectos');
            }else{
                return 
            }
        }
    }
}
</script>

<style scoped>

</style>