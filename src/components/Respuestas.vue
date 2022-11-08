<template>

  <section class="src-componentes-respuestas">
    
    <div class="jumbotron">
      <h2>Respuestas</h2>
      <br>

      <div class="table-responsive">
        <table class="table table-dark">
          <tr>
            <th>Número de pregunta</th>
            <th>Respuestas</th>
          </tr>
          <tr v-for="(elemento, index) in respuestas" :key="index">
            <td>{{ elemento.numero }}</td>
            <td>{{ elemento.valores }}</td>
          </tr>
        </table>
      </div>

    </div>
    
  </section>

</template>

<script>

  export default  {
    name: 'src-componentes-respuestas',
    props: [],
    mounted () {

    },
    data () {
      return {
        respuestas: [
        { numero: 1, valores: ['b', 'd'] },
        { numero: 2, valores: ['a', 'b', 'c'] },
        { numero: 3, valores: ['b', 'e'] },
        ]
      }
    },
    methods: {

    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  /*  .src-componentes-respuestas {

  } */

  .jumbotron {
    background-color: green;
    color: white;
  }
</style>
