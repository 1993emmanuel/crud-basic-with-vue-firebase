<template>
    <div id="login-component" class="container">
        <div class="row">
            
            <h1>Login</h1>
            <hr>

            <div class="col s12 m12" v-if="errors">
                <div class="card horizontal">
                    <div class="card-stacked">
                        <div class="card-content ">
                            <h5 class="center-align orange-text text-darken-2">Email // Password Invalidos</h5>
                        </div>
                    </div>
                </div>
            </div>


            <form class="col s12" @submit.prevent="loginForm" >
                <div class="row">
                    <div class="input-field col s12">
                        <input id="email" type="email" class="validate" v-model.trim="email">
                        <label for="email">Email</label>
                    </div>
                </div>
                <div class="row">
                    <div class="input-field col s12">
                        <input id="password1" type="password" class="validate" v-model.trim="pass">
                        <label for="password">Password</label>
                    </div>
                </div>
                <div class="row">
                    <button class="waves-effect waves-light btn-large" type="submit">Iniciar Session</button>
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
        pass : "",
        errors : false,
    }),
    methods:{
        async loginForm(){
            if(this.pass.length >= 6 && this.email!="" ){
                const API_KEY = "AIzaSyCSZKbeseFkGDvL1b6hpsB6Jim726wM_oI";
                // iniciar session
                try{
                    const respuesta = await fetch(`
                        https://identitytoolkit.googleapis.com/v1/accounts:signInWithPassword?key=${API_KEY}`,
                        {
                            method:'POST',
                            body : JSON.stringify({
                                email : this.email,
                                password : this.pass,
                                returnSecureToken : true
                        })
                    });
                    const data = await respuesta.json();
                    
                    if(data.error){
                        this.errors = true;
                    }else{
                        this.errors = false;
                        console.log(data);
                        localStorage.setItem('user',JSON.stringify(data))
                        router.push("/proyectos")
                    }

                }catch(error){}
                
            }else{
                return ;
            }
        }
    }
}
</script>

<style scoped>

</style>