<template>

  <section class="src-componentes-ingreso">
    <div class="jumbotron">
      <h2>Ingreso de Gastos</h2>
      <hr>

      <vue-form :state="formstate" @submit.prevent="enviar()">
        
        <validate tag="div">
          <label for="nombre">Nombre</label>
          <input 
          type="text"
          id="nombre"
          v-model.trim="formData.nombre"
          required
          name="nombre"
          autocomplete="off"
          class="form-control"
          :minlength="nombreMinLength"
          mayor-a
          no-espacios
          />
    
          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio</div>
            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo debe poseer al menos {{nombreMinLength}} caracteres.
            </div>
            <div slot="mayor-a" class="alert alert-danger mt-1">
              Este campo debe poseer menos caracteres.
            </div>
            <div slot="no-espacios" class="alert alert-danger mt-1">
              Este campo no admite espacios intermedios.
            </div>
          </field-messages>
        </validate>
        <br>

        <validate tag="div">
          <label for="descripcion">Descripción</label>
          <input
          type="text"
          id="descripcion"
          v-model="formData.descripcion"
          required
          name="descripcion"
          autocomplete="off"
          class="form-control"
          />
    
          <field-messages name="descripcion" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio</div>
          </field-messages>
        </validate>
        <br>
        
        <validate tag="div">
          <label for="importe">Importe</label>
          <input
          type="number"
          id="importe"
          v-model.number="formData.importe"
          required name="importe"
          autocomplete="off"
          class="form-control"
          />
    
          <field-messages name="importe" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio</div>
            <div slot="min" class="alert alert-danger mt-1">
              Este campo no puede contener números negativos
            </div>

          </field-messages>
        </validate>

        <br>

        <button class="btn btn-success my-3" :disabled="formstate.$invalid" type="submit">Enviar</button>
      </vue-form>
      <br>
      <hr>

      <h2>Detalle de Gastos</h2>
      <br>

      <h4><i>Presupuesto:</i></h4>
      <label for="presupuesto"></label>
      <input type="number" id="presupuesto" name="presupuesto" v-model="presupuesto">

      <br>
      <br>

      <div v-if="gastos.length" class="table-responsive">
        <table class="table">
          <tr>
            <th>Nombre</th>
            <th>Descripcion</th>
            <th>Importe</th>
            <th>Fecha</th>
          </tr>
          <tr v-for="(gasto,index) in gastos" :key="index">
            <td>{{ gasto.nombre }}</td>
            <td>{{ gasto.descripcion }}</td>
            <td> $ {{ gasto.importe }}</td>
            <td>{{ gasto.fecha }}</td>
          </tr>
          <tr>
            <td> </td>
            <td :style="{color: analizarTotal.color}">TOTAL</td>
            <td>$ {{total}}</td>
          </tr>
        </table>
      </div>
      <h3 v-else class="alert alert-info">No hay gastos ingresados</h3>

    </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-componentes-ingreso',
    props: [],
    mounted () {

    },
    data () {
      return {
        nombreMinLength: 3,
        formstate : {},
        formData : this.getInitialData(),
        gastos : [],
        total: 0,
        presupuesto: undefined,
      }
    },
    methods: {
      getInitialData() {
        return {
          nombre : null,
          dni: null,
          deuda: null,
          pago: null
        }
      },
      enviar() {
        let gasto = {...this.formData}
        gasto.fecha = new Date().toLocaleString()
        this.total += gasto.importe
        this.gastos.push(gasto)
        this.formData = this.getInitialData()
        this.formstate._reset()
      },
    },
    computed: {
      analizarTotal() {
        let color;
        const TOPE1 = 1000;
        const TOPE2 = 5000;

        if (this.presupuesto != undefined && this.presupuesto != 0 && this.presupuesto < this.total){
          color = 'red';
        } else {
          if (this.total <= TOPE1){
            color = 'green';
          } else if (this.total > TOPE1 && this.total <= TOPE2){
            color = 'magenta';
          } else {
            color = 'orange';
          }
        }
        //color = '#080'

        return {
          color
        }
      }
    }
}


</script>

<style scoped lang="css">
 /*  .src-componentes-ingreso {

  }
 */
  .jumbotron {
    background-color: lightyellow;
    color: brown;
  }

  hr {
    background-color: #eee;
  }

</style>
