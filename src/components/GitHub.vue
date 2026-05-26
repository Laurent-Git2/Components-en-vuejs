<template>

    <div class="container">
        <label for= "usuario">Nombre de usuario</label>
        <input id="usuario" type= "text"
            placeholder="Nombre de usuario"
            v-model="nombreusuario"
            @keydown.enter="obtenerUsuario"
            :disabled="cargando"
        >

    </div>
   
    <p v-if="errorVisible">

    Usuario no encontrado

</p>
    <div class="container" v-if="usuarioVisible">
        <h2>
            {{usuario.login}}
        </h2>
        
    <img
        :src="usuario.avatar_url"
        width="150"
    >
    <a :href= "usuario.html_url"> Perfil GitHub</a>
    <button @click="obtenerRepositorios">Repositorios</button>
    </div>

<div class="container" v-if="repositoriosVisible">

    <ul>

        <li v-for="repo in repositorios" :key="repo.id">

         <a :href="repo.html_url">
            {{ repo.name }}
        </a>

        </li>

    </ul>

</div>
</template>

<script>
export default {
    data() {
        return {
            nombreusuario: "",
            usuario:null,
            repositorios: [],
            errorVisible: false,
            usuarioVisible: false,
            repositoriosVisible: false,
            cargando: false

        }
    },
    methods: {
        async obtenerUsuario() {
            this.errorVisible= false
            this.usuarioVisible= false
            this.repositoriosVisible= false
            this.cargando= true

            const response = await fetch(
                `https://api.github.com/users/${this.nombreusuario}`
            )
        if(!response.ok)
        {
            this.errorVisible=true
            this.cargando=false
            return
        }
        const data= await response.json()
    this.usuario= data
    this.usuarioVisible= true
    this.cargando= false
        },

        async obtenerRepositorios() {

    this.cargando = true

    const response = await fetch(this.usuario.repos_url)

    const data = await response.json()

    this.repositorios = data

    this.repositoriosVisible = true

    this.cargando = false
}
    }
}
</script>

<style scoped>
.container
{
    padding: 15px;
    margin: 15px;
}
div {

    display: flex;

    flex-direction: column;

    align-items: center;
}

label {

    font-size: 25px;

    margin-bottom: 10px;
}

input {

    font-size: 20px;

    width: 300px;

    padding: 10px;
}
</style>