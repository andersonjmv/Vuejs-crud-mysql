<template>
  <div class="container">
    <div class="card">
      <div class="card-header">Empleados</div>
      <div class="card-body">
        <table class="table">
          <thead>
            <tr>
              <th>id</th>
              <th>nombre</th>
              <th>correo</th>
              <th>acciones</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="empleado in empleados" :key="empleado.id">
              <td>{{ empleado.id }}</td>
              <td>{{ empleado.nombre }}</td>
              <td>{{ empleado.correo }}</td>
              <td>
                <div class="btn-group" role="group" aria-label="">
                  <router-link :to="{name:'Editar',params:{id:empleado.id}}" class="btn btn-info">Editar</router-link>
                  <button type="button" v-on:click="borrarEmpleado(empleado.id)" class="btn btn-danger">Borrar</button>
                </div>

              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      empleados: [],
    };
  },

  created: function () {
    this.consultarEmpleados();
  },
  methods: {
    consultarEmpleados() {
      fetch("https://localhost/empleados/")
        .then((respuesta) => respuesta.json())
        .then((datosRespuesta) => {
          //console.log(datosRespuesta);
          this.empleados = [];
          if (typeof datosRespuesta[0].success === "undefined") {
            this.empleados = datosRespuesta;
          }
        })
        .catch(console.log);
        
    },
    borrarEmpleado(id){
      
      fetch("https://localhost/empleados/?borrar="+id)
        .then((respuesta) => respuesta.json())
        .then((datosRespuesta) => {
          console.log(datosRespuesta);
          window.location.href="Listar"
        })
        .catch(console.log);
    }
    
  }
};
</script>