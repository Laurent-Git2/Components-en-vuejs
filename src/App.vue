<template>
  <div>
  <h1>Buscar Usuarios GitHub</h1>
  <GitHub/>
  </div>
</template>

<script>
import GitHub from "./components/GitHub.vue"
export default
{
  components: 
  {
    GitHub
  }
}
</script>
<style scoped>
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
